# Day 3 - Ruby Koans

## Learning Objectives/Competencies

1. Students will be able to setup their preferred IDE and integrate it with Ruby and Rails.
1. Students will gain familiarity "thinking in Ruby" by implementing a [Ruby Koan](http://rubykoans.com/).

## Initial Exercise: Environment Setup (25 Minutes)

Direct students to **read and complete _one_ of the following tutorials**, based on their editor of choice:

- **Atom**: [Atom Tricks for Ruby Developers](https://www.rubyguides.com/2017/11/atom-tricks-for-ruby-developers/)
- **VSCode**: [Ruby on Rails with Visual Studio Code](https://medium.com/@PaulWritesCode/ruby-on-rails-with-visual-studio-code-bc5681a2c098)

## Overview/TT I

Today's class focuses on **solving problems using the Ruby language**. In order to achieve this, we'll complete a few in-class challenges that solving a [Ruby Koan](http://rubykoans.com) of your choice.

### Why Koans?

> The Koans walk you along the **path to enlightenment** in order to **learn Ruby**. The goal is to **learn the Ruby language, syntax, structure, and some common functions and libraries**. We also teach you **culture**. **Testing** is not just something we pay lip service to, but something we live. It is **essential in your quest to learn** and do great things in the language.

### Discovering the Path to Enlightenment

> The koans are broken out into areas by file, hashes are covered in `about_hashes.rb`, modules are introduced in `about_modules.rb`, etc.

> They are presented in order in the `path_to_enlightenment.rb` file.

> Each koan **builds up your knowledge of Ruby** and **builds upon itself**. It will **stop at the first place you need to correct**.

> Some koans simply need to **have the correct answer substituted for an incorrect one**. Some, however, **require you to supply your own answer**. If you see the method `__` (a double underscore) listed, it is a **hint** to you to **supply your own code in order to make it work correctly**.

## In Class Activity I: Starting the Journey

1. Run the following code in your terminal _after_ forking this repository. **Make sure to replace the clone link in the first instruction with your fork!**

    ```bash
     git clone git@github.com:droxey/BEW-1.3-Server-Side-Architectures-and-Frameworks.git
     cd BEW-1.3-Server-Side-Architectures-and-Frameworks/Materials/koans
    ```

1. Execute the `path_to_enlightenment.rb` script. You should receive the following output:

    ```bash
    $ ruby path_to_enlightenment.rb

    AboutAsserts#test_assert_truth has damaged your karma.

    The Master says:
      You have not yet reached enlightenment.

    The answers you seek...
      Failed assertion.

    Please meditate on the following code:
      /Users/droxey/dev/repos/BEW-1.3-Server-Side-Architectures-and-Frameworks/Materials/koans/about_asserts.rb:10:in `test_assert_truth'

    mountains are merely mountains
    your path thus far [X_________________________________________________] 0/282
    ```

## BREAK (10 Minutes)

## After Class

- Continue working on the [Ruby on Rails Guides Tutorial](https://guides.rubyonrails.org/getting_started.html).

## Additional Resources

1. [Ruby Koans](http://rubykoans.com/)
