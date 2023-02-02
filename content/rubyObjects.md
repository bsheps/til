---
title: "Ruby: everything is an object"
date: 2023-02-02T13:11:00+08:00
draft: false
tags: ['ruby', 'OOP', 'programming languages', 'Software']
---

Today was my first time tinkering with Ruby. I was surprised to learn that almost everything is an object, and accessing all of the encapsulated methods was a simple dot method `.methods` call away.

```ruby
# Here's an example using Ruby's command line interpreter (aka "irb_prompt" below):

# Numbers are objects by default.

irb_prompt> 4
=> 4

irb_prompt> 4.class
=> Integer

irb_prompt> 4.methods
=> [:-@, :**, :<=>, :<=, :>=, :==, :===, :eql?, :%, :inspect, :*, :+, :-, :/, :<, :>, :to_int, :coerce, :to_s, :divmod, :to_i, :to_f, :to_r, :fdiv, :modulo, :abs, :magnitude, :zero?, :finite?, :infinite?, :floor, :ceil, :round, :truncate, :positive?, :negative?, :numerator, :denominator, :rationalize, :arg, :hash, :angle, :phase, :quo, :nan?, :next_float, :prev_float, :+@, :singleton_method_added, :i, :remainder, :real?, :integer?, :nonzero?, :step, :clone, :dup, :rect, :real, :imaginary, :imag, :abs2, :conjugate, :rectangular, :to_c, :polar, :conj, :div, :between?, :clamp, :instance_variable_defined?, :remove_instance_variable, :instance_of?, :kind_of?, :is_a?, :tap, :instance_variable_get, :instance_variable_set, :instance_variables, :singleton_method, :method, :public_send, :define_singleton_method, :public_method, :extend, :to_enum, :enum_for, :=~, :!~, :respond_to?, :freeze, :object_id, :send, :display, :nil?, :class, :singleton_class, :itself, :yield_self, :then, :taint, :tainted?, :untaint, :untrust, :untrusted?, :trust, :frozen?, :methods, :singleton_methods, :protected_methods, :private_methods, :public_methods, :equal?, :!, :__id__, :instance_exec, :!=, :instance_eval, :__send__]

irb_prompt> 4.positive?
=> true

# This object paradigm works with decimals...

irb_prompt> 4.1.class
=> Float

irb_prompt> 4.1.ceil
=> 5

irb_prompt> 4.1.floor
=> 4

# and booleans are objects too

irb_prompt> true.class
=> TrueClass
```

"Everything as an object" paradigm seems really friendly from a programmer perspective, but isn't this a waste in terms of memory inefficiency?