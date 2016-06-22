---
title: Project Euler Type Ruby Questions
excerpt:
author: Ryan Johnson
categories:
  - topics
#date/lastupdated are optional
#date: 2016-06-20 22:14:03
#lastupdated: 2016-06-20 22:14:03
---
Anyone with familiarity of Ruby knows basic conditionals (if, else, while) and methods of iteration (.each do |i|). What really gets the brain cells firing is a set of Ruby puzzles known as <a href="https://projecteuler.net/">Project Euler</a>. These computational logic questions can trip up a developer with plenty of Rails/JavaScript experience (me) but not enough time spent understanding computational problems (me again).

I spend the past couple days breaking down how to solve these types of problems. Let's start with the premise, <b>find the second largest number in a list</b>. Oh, and to make it beyond a one-line challenge, do it without using Ruby's sort method. How do we solve that? Like any big problem, let's begin by breaking it down.

#Need two variables, max_so_far and max_second
Step outside the world of coding an imagine you're doing down a list of basketball players with their jersey numbers. If you wanted to return the highest number, you'd start with the first number, let's say it's 14, then you'd move to the next number, say 44, and ask is first number (14) greater than next number (44). If the next number is greater than the previous number we want to replace the second number with the first.

Even though the language above is written in basic English and pseudocode, the keywords describe just what we're looking for.
First number and next number <- going to need two variables
"Is first number greater than next number" <- require > variables
"If the next number is greater...replace" <- if conditional needed

This is a great starting point to begin with what we know.

Assuming we work with all positive integers (as far as I know there's no negative jersey numbers) we can set two variables max_so_far (the biggest number found in the list) and max_second (the second biggest number) as '-1' which essentially renders them nil. Knowing to place all the logic inside a method, an appropriate name would be max, taking an argument of list.

<xmp>
def max(list)
  max_so_far = -1
  max_second = -1
end
</xmp>

Now it's time to iterate over the list. Taking the argument, we'll run Ruby's .each method to run over all the items in the list.

<xmp>
def max(list)
  max_so_far = -1
  max_second = -1

  list.each do |l|
  end
end
</xmp>

Another step closer. Here's the tricky part, so let's start by finding the largest number.

<xmp>
def max(list)
  max_so_far = list.first
  list.each do |l|
    if l > max_so_far
      max_so_far = l
    end
  end
  max_so_far
end

</xmp>

Boom! The logic checks if l > max_so_far and if so, assigns max_so_far to the value of l. After we leave the loop, we return the value of max_so_far. Let's check that by running a the function. Add this final line.

<xmp>
max([1, 4, 5, 7, 9])
</xmp>

Save the file as a .rb extension, then run 'ruby [file name].rb'. You should get the output '9', the largest number. Now to get the second highest number. After the if conditional checking the list, set max_second equal to max_so_far. This will take the max_so_far that's stored in memory (i.e. the second highest number).

<xmp>
def max(list)
  max_so_far = -1
  max_second = -1

  list.each do |l|
    if l > max_so_far
      max_second = max_so_far
      max_so_far = l
    end
  end

end

puts max([1, 4, 2, 6, 0])
</xmp>

Getting warmer. Branch out an else conditional to check if l is greater than max_second.

<xmp>
def max(list)
  max_so_far = -1
  max_second = -1

  list.each do |l|
    if l > max_so_far
      max_second = max_so_far
      max_so_far = l
    else
      if l > max_second
        max_second = l
      end
    end
  end

end

puts max([1, 4, 2, 6, 0])
</xmp>

Cha-ching! That's now working code to check the second largest number in a list.
