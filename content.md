# Each

When we met the `Array` class, we noted that most of what we do as developers is manage _lists of things_ — photos, likes, followers, reviews, listings, messages, rides, events, concerts, projects, etc etc etc — and `Array` is the data structure that we'll most commonly use to contain these lists.

Therefore, the most common reason we'll have to write loops is to **visit each element in an `Array` and do something interesting with it** — for example, display the element to the user with some formatting around it.

- Quick quiz. Which of these would result in an `Array` class object in the variable `a`? Select all that apply, and use the empty runnable code block below if you want for testing.
- `a = ()`
    - No, parentheses are used after a method to list the arguments to the method
- `a = Array`
    - No, what method do we need to call _on_ `Array` to create a new one?
- `a = []`
    - Yes! Thanks to some syntactic sugar
- `a.new = Array`
    - No, the method should be on the right side of the assignment operator
- `a = Array.new`
    - Yes!
- `a = "ruby".split("")`
    - Yes! The `""` argument to `split` will separate each character
- `a = [1, 2, 3]`
    - Yes!
{: .choose_all #arrays title="Array review" points="4" answer="[3,5,6,7]" }

```ruby
# test your knowledge
```
{: .codeblock #testing_arrays title="Test runnable code block"}

## Iterating over arrays with Integer's times method

Let's try transforming the words in an `Array` using what we've learned so far about loops. This program takes a list of words and prints each word in three forms:

```ruby
words = ["apple", "banana", "orange"]
number_of_words = words.count

number_of_words.times do |the_index|
  pp words.at(the_index).capitalize
  pp words.at(the_index).reverse
  pp words.at(the_index).upcase
end
```
{: .codeblock #three_forms_times title="Three forms with times" points="1"}

You see that I chose to use `.times` for this job.

 - On Line 2, we count the length of the array.
 - On Line 4, we use that length with the `.times` method to kick off a loop with the correct number of iterations.
 - Within the block, we use the block variable (which we named `the_index`) to access the correct element within the array.
 - We printed the array element capitalized, reversed, and then upcased.

Using `.times` to iterate over an `Array` is not bad at all, especially because `.times`'s block variable starts at `0`, just like array indexing does. Using `.times` is certainly cleaner than using `while`, where we would have to create and increment a counter variable ourselves, and then write a condition to make sure that the loop stops after the correct number of iterations (the length of the array).

## Array's each method

But we can do even better than using `Integer`'s `.times` (or `.step`) method to iterate over an `Array`. There's a method that you can call directly on the `Array` itself called `.each`. Compare the code below to the previous runnable code block and try to find the differences:

```ruby
words = ["apple", "banana", "orange"]

words.each do |the_word|
  pp the_word.capitalize
  pp the_word.reverse
  pp the_word.upcase
end
```
{: .codeblock #three_forms_each title="Three forms with each" points="1"}

Click "Run" and verify that both programs do the same thing.

Nice! `.each` has two clear benefits over using `.times`:

 - We don't need to count the length of the array; `.each` does it for us and will take care of looping for the correct number of iterations.
 - The block variable, rather than containing an integer that we can use to access the correct element, will contain **the element itself**.

     So now when we name the block variable, we should choose a name that reflects what each element in the list is.

     `.each` will, behind the scenes, pull the correct element out of the array before each iteration begins and assign it to that block variable.

     Then, **we just use that variable directly**, and we don't have to worry about accessing the array with `.at`.

<aside>
I like to name the variables that contain arrays _plurally_ (e.g. `photos`), and block variables _singularly_ (e.g. `photo`) to make it clear to myself which is which — the list itself versus one element within the list. Whatever you do, don't name the block variable plurally — that's very confusing when you come back to your code later and have to make sense of it.
</aside>

The hardest part, I think, is getting your head around the block variable; in this case, `|the_word|`. It takes some practice.

Try to remember that it's just a name that _we make up_, and `.each` takes care of putting each element in that variable for us behind the scenes. I could have called it `zebra` if I wanted to; there's nothing special about the name of the variable — in particular, it doesn't have to match the name of the variable containing the array (`words`). Just try to pick something descriptive of an individual element in the list.

## Practice using each

Looping over lists of things with `.each` is _very_ important for us. Let's get some practice writing small programs using `.each` and `|block_variables|` in the next three graded code blocks.

### Spell this word

Write a program that, given a randomly `sample`d `word` from the list, spells it out letter-by-letter, with capital letters. For example, if the `word = "Georgia"`, the output should be:

```
"G"
"E"
"O"
"R"
"G"
"I"
"A"
```

Hint: recall, `.split("")` will separate a `String` into an `Array` of characters, so you can write `word.split("").each ...` to start your program.

```ruby
word = ["Ruby", "application", "zebra"].sample
# write your program here
```
{: .codeblock #spelling title="Spelling" readonly_lines="[1]" points="1"}

```ruby
describe "Spelling" do
  it "should print ''S' 'U' 'P' 'E' 'R'' if the input is 'Super'" do
    replace_read_only_value(variable_name: "word", new_value: "Super")
    output = run_codeblock
    expect(output).to fuzzy_match("S U P E R")
  end
end
```
{: .codeblock-test #spelling_test_1 for="spelling" title="Spelling should print ''S' 'U' 'P' 'E' 'R'' if the input is 'Super'" points="1"}

### Even word

Now write a program that, given the `list_of_words`, only prints the words that have an even number of characters. For example, if the list was `["mountain", "pink", "vines"]`, the output should be:

```
"mountain"
"pink"
``` 

Hint: remember you can nest `if`-`else` conditionals inside of loops.

Note: be sure to use `pp` to print the output (do not use `p` or `puts`; alternative printing methods).

```ruby
list_of_words = ["zebra", "giraffe", "monkey", "salmon"]
# write your program here
```
{: .codeblock #even_words title="Even words" readonly_lines="[1]" points="1"}

```ruby
describe "Even words" do
  it "should print 'monkey salmon'" do
    failure_if_literally_printing("monkey")
    failure_if_literally_printing("salmon")
    output = run_codeblock
    expect(output).to fuzzy_match("monkey salmon")
  end
end
```
{: .codeblock-test #even_words_test_1 for="even_words" title="Even words should print 'monkey salmon'" points="1"}

```ruby
describe "Even words" do
  it "should print nothing if the input is ['odd', 'numbers', 'squad']" do
    replace_read_only_value(variable_name: "list_of_words", new_value: ["odd", "numbers", "squad"])
    output = run_codeblock
    expect(output).to match("")
  end
end
```
{: .codeblock-test #even_words_test_2 for="even_words" title="Even words should print nothing if the input is ['odd', 'numbers', 'squad']" points="1"}

### Letter count

Finally, use `.each` to write a program that, given a randomly `sample`d `word` from the list, prints each letter in the word, and the number of times that letter appears. For example, if `word = "loop"`, the output of your program should be:

```
"l appears 1 times"
"o appears 2 times"
"o appears 2 times"
"p appears 1 times"
``` 

Hint: recall, `.split("")` will separate a `String` into an `Array` of characters, and `.count(<character>)` will count the number of occurrences of a given character in a `String`.

Note: be sure to use `pp` to print the output (do not use `p` or `puts`; alternative printing methods).

```ruby
word = ["photo", "like", "commenter"].sample
# write your program here
```
{: .codeblock #letter_count title="Letter count" readonly_lines="[1]" points="1"}

```ruby
describe "Letter count" do
  it "should print the correct output for 'loop'" do
    replace_read_only_value(variable_name: "word", new_value: "loop")
    output = run_codeblock
    expect(output).to fuzzy_match("l appears 1 times o appears 2 times o appears 2 times p appears 1 times")
  end
end
```
{: .codeblock-test #letter_count_test_1 for="letter_count" title="Letter count should print the correct output for 'loop'" points="1"}

```ruby
describe "Letter count" do
  it "should print the correct output for 'levee'" do
    replace_read_only_value(variable_name: "word", new_value: "levee")
    output = run_codeblock
    expect(output).to fuzzy_match("l appears 1 times e appears 3 times v appears 1 times e appears 3 times e appears 3 times")
  end
end
```
{: .codeblock-test #letter_count_test_2 for="letter_count" title="Letter count should print the correct output for 'levee'" points="1"}

## Sneak peek

Just a sneak peek as to why `.each` is so important to get comfortable with: soon, you'll be embedding Ruby loops in your web applications to create dynamic, data-driven pages with code that looks something like this:

```erb
<% newsfeed_photos.each do |the_photo| %>
  <div class="card">
    <img src="<%= the_photo.image_source %>">

    <p>
      <%= the_photo.caption %>
    </p>
  </div>
<% end %>
```

Code like this is what drives the dozens of dynamic applications you interact with on a daily basis — we pull a list of records from a database table, then we loop over them, and then we format each one using some _markup language_ (in this case HTML for the browser, but it could be XML for native apps, etc).

##  Conclusion

That's it for `.each` and loops. It's time to meet a very important data structure class that we will be seeing a lot: `Hash`.

- Approximately how long (in minutes) did this lesson take you to complete?
{: .free_text_number #time_taken title="Time taken" points="1" answer="any" }

