---
layout: post
title: Hash Traversal in Perl 
comments: true
tags: [ tutorial, perl, programming tricks, hash ]
---

Today, I wanted to talk about hash traversal in Perl with the aim of flattening a complex multi-level hash into a simpler single-level hash. Hash traversal is a perfect way to get some practice with recursion in, so we will be using that approach here as well. Let's outline how this might look:

1. Inputs
2. Iterate over original hash
3. Recursion!
4. Flattening

We can choose to flatten in any way we want. Since this was originally conceived to work with MongoDB queries (specifically to assist in accessing values in complex objects), we will join the keys down to the final key with a period (`.`).

## Inputs

Since we will be writing a recursive function, we know we will at least have to take as an input the next level of hash available (we will be doing a depth-first traversal). Since we need to keep track of every level we get into for flattening, we should also keep track of the keys through each call. Another hash reference, which we will call `output`, will also need to be passed in to each recursive call, which will be loaded with our key-value pairs as we unwind the stack.

This will be a special, unnamed parameter, and will be `undef` on the call your program makes to `flatten_hash`. So the parameters we will pass in to our function will be the undefined output, your input hash, and an initially empty arrayref that will keep track of the keys that point to subhashes. 

{% highlight perl %}
# Named inputs: original_hash, keys_list
sub flatten_hash {
    my %output = %{shift @_};
    my %args = @_;
}
{% endhighlight %}

## Iteration

As a necessity, we need to iterate over the keys of the hash we are working on. Instead of the more common `foreach my $key (keys %hash)` idiom, we will instead use the `each` built-in. There are some [arguments against using each](http://blogs.perl.org/users/rurban/2014/04/do-not-use-each.html), which include the fact that the `each` internals can get confused if the original hash is modified while being iterated through. Luckily, that doesn't cover our use case, and `each` is fine to use here. Use caution with it in general, though. 

`each` returns to us the key and value of each element of a hash. We will unpack those results as we iterate, and also set up the recursive call and the list of previous keys. 

{% highlight perl %}
while (my ($key, $value) = each(%{$args{original_hash}})) {
    my @data_address = defined($args{keys_list}) ? @{$args{keys_list}} : ();
    push(@data_address, $key);
}
{% endhighlight %}

Notice the [ternary operator](https://perlmaven.com/the-ternary-operator-in-perl) - if the `keys_list` parameter is defined, we will dereference it and set it to `@data_address`, otherwise we will initialize `@data_address` as an empty array. We will then `push` the current key we're on to the end of the `@data_address` array. 

## Recursion

We looked a little bit at the `$key` part of the `each` call's results, but let's take a look at the `$value` return. If we're examining a multi-level hash, there will be occasions where `$value`'s type is a hashref, instead of a scalar. That indicates to us that there is more to explore -- we have arrived at our recursive case.

{% highlight perl %}
if (ref($value) eq 'HASH') {
    %output = flatten_hash(\%output, original_hash => $value, keys_list => \@data_address);
}
{% endhighlight %}

## Flattening

If `$value` is not a reference to a hash, then we're in our base case (you can expand the recursive case check to include arrays, but I'll leave that as an exercise to the reader) - `$value` is an actual scalar value. 

{% highlight perl %}
else {
    my $addr = join('.', @data_address);
    $output{$addr} = $value;
}
{% endhighlight %}

Here, we join all the keys leading to this particular piece of data with a period. We can do this with whatever delimiter you need for your specific application. Then we use autovivification to add to the `%output` hash the new combined key and then assign it the value stored in `$value`. All that is left is to return `%output`, which you can see in the final code below:

{% highlight perl %}
sub flatten_hash {
    my %output = %{shift @_};
    my %args = @_;
    while (my ($key, $value) = each(%{$args{original_hash}})) {
        my @data_address = defined($args{keys_list}) ? @{$args{keys_list}} : ();
        push(@data_address, $key);

        if (ref($value) eq 'HASH') {
            %output = flatten_hash(\%output, original_hash => $value, keys_list => \@data_address);
        }
        else {
            my $addr = join('.', @data_address);
            $output{$addr} = $value;
        }
    }
    return %output;
}
{% endhighlight %}

Here is a quick test script that shows how to use this method and what its output looks like.

{% highlight perl %}
#!/usr/bin/perl
use strict;
use warnings;
use Data::Dumper;

my $test_hash = {
    a => 'a',
    b => {
        d => 'd',
        e => 'e',
        f => {
            g => 'g',
            h => 'h',
        },
    },
    c => 'c',
};

my %empty;
my %res = flatten_hash(\%empty, hashref => $test_hash, arguments => []);
print "Test hash:\n";
print Dumper($test_hash);
print "Result\n";
print Dumper(\%res);
{% endhighlight %}

This code grew out of modifications I made to the excellent answer given in [this Stack Overflow answer](http://stackoverflow.com/questions/160175/traversing-a-multi-dimensional-hash-in-perl), which gives a basic template to traversing a hash with a callback in Perl. 