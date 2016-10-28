---
layout: post
title: Hash Slices in Perl 
comments: true
tags: [ tutorial, perl, programming tricks, hash ]
---

Recently, I had a bug at work that would be solved by simply stripping certain characters from the keys of a hash. This seems easy at first: iterate through the keys with the `keys` operator and run a regex substitution on that, something like the following (with the goal of stripping periods):

{% highlight perl %}
my $my_hash = ('al.pha' => 'a', 'beta' => 'b');

s/\.*//g foreach keys %my_hash;
{% endhighlight%}

For those deeply familiar with Perl, the error probably seems obvious - `keys` doesn't return references to the keys in the hash for you to manipulate in place, it instead returns copies of the keys. These copies are what we're iterating through with `foreach` and stripping the period from. 

If we use `Data::Dumper` on `%my_hash`, we will be greeted with the hash in its original state:
```
$VAR1 = {
          'al.pha' => 'a',
          'beta' => 'b'
        };
```

But if we instead print the default variable within the foreach after the substitution with a little code reorganization:
{% highlight perl %}
foreach (keys %hash) {
    s/\.*//g;
    print "Default var: $_\n";
}
print Dumper(keys %hash);
{% endhighlight%}

This is our output:
```
Default var: a
Default var: alpha
$VAR1 = 'al.pha';
$VAR2 = 'a';
```

So the values in `$_` were correctly stripped of periods, but the actual keys in the hash were unaffected. Let's continue on this path (using the substitution operator `s///` with a `foreach`) - if you have used Perl for any appreciable amount of time, you know TIMTOWTDI (pronounced "Tim Toady": **t**here **i**s **m**ore **t**han **o**ne **w**ay **t**o **d**o **i**t) is a guiding philosophy behind Perl, and there are a number of ways to tackle a problem like this. We will be continuing the use of `keys`, though. Since `keys` returns a copy of a hash's keys, we can load it into a new array:
{% highlight perl %}
my @new_keys = keys %my_hash;
{% endhighlight%}

Easy enough. Now we can iterate over this and use the substitution operator to substitute in place:
{% highlight perl %}
s/\.*//g foreach @new_keys;
{% endhighlight%}

Here comes the perl magic, can you see all the things that are accomplished in this one line? 

{% highlight perl %}
@my_hash{@new_keys} = delete @my_hash{keys %my_hash};
{% endhighlight%}

Here we finally make use of [hash slices](http://perldoc.perl.org/perldata.html#Slices) - twice, in fact. Both times that we encounter `my_hash`, it's in a list context, as are the keys that we are addressing. This technique allows us to operate on or assign to a list of keys all at once. So `@my_hash{keys %my_hash}`, in the state it is in now, gives us a list of all the values that are in `my_hash`. Why are we calling `delete` on those, though? `delete` has an interesting side effect beyond deleting things: `delete` also returns what it is deleting. 

So not only do we delete the old values from the hash, we load them in to the appropriate new keys, all in one line! We can also guarantee that the values get loaded into the correct keys. This is because `keys` returns [entries in the same random order for the same hash](http://perldoc.perl.org/functions/keys.html). This depends on the hash not changing between calls to `keys`. 

To put it all together, we have three lines (any wizards want to make it even shorter?) that, in effect, will run a regex substitution on all keys of a hash, seemingly in place. 

{% highlight perl %}
my @new_keys = keys %my_hash;
s/\.*//g foreach @new_keys;
@my_hash{@new_keys} = delete @my_hash{keys %my_hash};
{% endhighlight %}

And the results:
```
$VAR1 = {
          'alpha' => 'a',
          'beta' => 'b'
        };
```

Success!