---
layout: post
title: "Expressive Code"
date: 2015-06-14 15:40:37 -0400
comments: true
categories: 
---

Two weeks ago I started learning Ruby at the Flatiron School. In that time we’ve gone over the basics of the language. One of the things that I love about Flatiron is that they teach the mechanics behind the language and the thinking behind the mechanics. When I was teaching myself, I was able to make things work, but I didn’t necessarily understand how or why they worked.

Ruby is a very expressive language. Its expressiveness comes from its creator’s human-centric philosophy about the purpose of programming languages: that they should be built to serve the people that use them, rather than the machines that take their orders. To quote <a href="http://mislav.uniqpath.com/poignant-guide/book/chapter-3.html">_why</a>, "We can no longer truthfully call it a computer language. It is coderspeak. It is the language of our thoughts.” 

After just two weeks, I’ve already been having odd dreams where the Each enumerator repeats like a mantra throughout. Each… do. Each… do. At the height of my struggles iterating through nested hashes, I dreamt I was hosting a get together at my apartment. Each person. Do greet if not_greeted == true. Each person. Do favorite_drink. guests.each { |guest| guest += favorite_drink }.  

I’m only just beginning to get familiar with Ruby, but I’ve learned that part of its simplicity and human-readability-ness comes from abstraction and syntax. The more we can abstract away and compartmentalize the levers that make our code work, the better our code will read. And ultimately, code is not just for computers. It’s also for the people that have to write it, read it, and improve upon it. In Ruby, Enumerators allow us to, among other things, hide the plumbing of our code and replace it with simpler statements. 

Take Each, the enumerator that's invaded my dreams. Each takes a collection of data and loops through each of its individual data points, allowing us to perform an action using every piece of data individually. Keeping with the example from my dream, let’s say I have an array of guests [“John”, “Paul”, “George”, “Ringo"], and I want to make sure that my program says “Hi” to each of them. My code will have to go into the array of guests, choose the person that I want to greet, greet them, and repeat until all of the guests have been greeted. Without enumerators, my code would look like this:
<pre><code>
# simple iteration
i = 0
while i < guests.count
  puts “Hi #{guests[i]}!”
  i += 1
end
</code></pre>

I have to set an index to keep track of which guest I’m greeting and how many guests I’ve greeted. The code explicitly increments the index after saying hi to each guest. 

Performing the same task with the Each enumerator allows me to abstract out the index and incrementation because Each keeps track of the counting for me. It looks like this:
<pre><code>
# iteration with each
guests.each do |guest|
  puts “Hi #{guest}!”
end
</code></pre>

Much simpler. I went from 5 lines of code to three, and in the process we removed the explicit incrementation. It’s also much easier to read. So how does Each work? 

Each leverages Blocks and Yield. Behind the scenes, Each is keeping track of how many items it’s iterating through, and passing the data from each iteration through to a separate set of actions defined by the block (the area between do and end above). Written out, Each on its own looks something like this:
<pre><code>
# mechanics of each
i = 0
while i < data.count
  yield
  i += 1
end
</code></pre>

Here we have the same counter as before, and the only thing that’s happening besides incrementing the counter is that we’re calling yield. Yield sends the data to a Block (the do … end statement) where another set of code is enacted. In our example, each is being called on guests and passing each guest through to the block we define (do |guest| “puts 'Hi #{guest}!’” end). This is the beauty of enumerators. All of this happens behind the scenes - we’ve abstracted out the incrementation to create a much simpler operation: Each. Ultimately, enumerators are powerful because they make code simpler and thereby easier to read, manage, and write. 
