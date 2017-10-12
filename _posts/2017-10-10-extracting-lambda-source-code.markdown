---
layout: 'post'
title: 'Extracting Lambda Source Code'
date: 2017-10-10
author: 'Danilo Barion Nogueira'
excerpt: 'In this post, I’ll show you how to extract the code definition of a Lambda object, using just pure Ruby!'
twitter: 'https://twitter.com/daniloinfo86'
github: 'https://github.com/danilobarion1986'
website: 'https://devdanilo.wordpress.com/'
---

In this post, I’ll show you how to extract the code definition of a Lambda object, using just pure Ruby!

But, first things first! What is a lambda in Ruby? A lambda is an special type of Proc, with some little differences in syntax, behavior and functionality, one of them that could be used as an anonymous function. There are many articles with all the details of what a lambda is and its main differences from a Proc and a block, one of them is [this](http://culttt.com/2015/05/13/what-are-lambdas-in-ruby.).

At one of my side-projects, I wanted to extract the definition of one property of my class, that is a lambda defined by the user, and make a little markdown documentation page with this code on it. Then I thought: “Well, Ruby must have some special method call to do this… Or maybe the object itself (lambda) has an to_s like method that returns its own definition...”. But, well, for my surprise it was not so simple...

## Trying some code…

Then, I googled a little bit, and found some gems that works, but honestly, it’s a so tiny part of my project that I don’t wanted to add an entire extra-project just to extract source code from an lambda object… Besides this, my goal is to make a gem that don’t have third-party dependencies at all…

Then, after some reading, coding, testing, refactoring, this was my result:

```ruby
class LambdaReader
  class << self
    # Receive an lambda object and returns its source code as string or nil if not valid
    def lambda2source(obj)
      unless obj.class == Proc
        raise ArgumentError,
              "Wrong parameter class. Expected Lambda, got #{obj.class}."
      end
      @lambda_code_line = extract_lambda_code_line(obj.source_location)
      lambda_code = match_lambda_syntax
      lambda_code[0] unless lambda_code.nil?
    end

    private

    # read the file where the lambda was defined and
    # extract the text of the entire line
    def extract_lambda_code_line(lambda_source_location)
      file_name = lambda_source_location.first
      line_number = lambda_source_location.last
      IO.readlines(file_name)[line_number - 1]
    end

    # extract the lambda definition using regexes
    # to capture one of the 2 syntax that can be
    # used to define lambdas in Ruby
    def match_lambda_syntax
      classic_syntax_matcher || dash_rocket_syntax_matcher
    end

    # match the "classical" syntax for lambdas
    # lamda { |x| puts x } or lambda { puts 'ok' }
    def classic_syntax_matcher
      /lambda ?{ ?\|.*\|.*}/m.match(@lambda_code_line)
    end

    # match the "dash rocket" syntax for lambdas
    # -> (x) { puts x } or -> { puts 'ok' }
    def dash_rocket_syntax_matcher
      /-> ?\(.*\) ?{.*}/m.match(@lambda_code_line)
    end
  end
end
```

It’s a simple class, with one public method (lambda2source), that receives the lambda object and returns its source code as string.

If the passed parameter it’s not an lambda, it raises an ArgumentError exception, with an informative message. Else, it checks what syntax was used to define the lambda (matching one of the two possibilities). This return is already the source code that I want to use.

## Cons

With this approach, I could easily retrieve the code that I want, without using any third-party code/gem get this functionality in my project.

Even though is a simple solution, we have some limitations like, for example, it’s not possible to extract the source code of lambdas defined at runtime. But, for my needs it’s enough.

So, I have a solution that is simple and I don’t need to worry with some dependency that might break one of the main features that I want to provide, that is auto-generated documentation!


*Did you like this article? Are you careful about add third-party code to your applications too? Have any comments, suggestions or critics?*

*Until next post!*
