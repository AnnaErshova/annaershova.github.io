When one first starts coding, the main concern is writing something that works and produces desired result.

You get irb to output "Hello World!" -- excellent. Then you get a nested hash-array monster to return a very specific key hidden 7 levels deep -- great. Then you write your CLI interface that runs in your command line and shows scraped data from your fellow students' bio -- good job. And you even use cowsay to format interactions with the user and format command line output using escape sequences, so that user interface looks less boring. And when you hit rspec, most tests pass.

And then the next task comes -- how do you make your actual code look good? 

>“Code so beautiful that tears are shed.” 

*Why’s Poignant Guide to Ruby*

So how do you write code that indeed is so beautiful and elegant that tears will be shed by those reading your pull request?

There are multiple parts to the puzzle, but let's start with aesthetics of formatting first.

Do you remember when Avi said that he had been looking at our code, and we all needed to abide by basic indentation and not leave not-working code bits floating around commented out?

Ruby is perfectly fine with reading your code without any and all indentations and any real formatting. It can easily ignore all the hashed-out random comments. But once the code we read and write gets more and more complex, us humans really benefit from proper formatting to figure out what goes where -- especially when the code is revisited at a later point and no one remembers anymore what it was really supposed to do. 

To use proper formatting is also kind to anyone who might work on the code after you, so that they won't have to spend hours doing forensic coding and figuring out what end statement closes what block. 

And it is simply and elegant thing to do. And it's Step 1 to Writing Elegant Code.

You know how when you went to college you had to format your essay footnotes a very specific way using a style manual or a helpful website or two? Well, there is a Ruby style manual, too!

<a "href=https://github.com/airbnb/ruby">The Airbnb Ruby Style Guide</a> is what I suggest as a reference for all the formatting questions that are keeping you up at night.(Airbnb website is in Ruby and Ruby on Rails by the way -- see, real companies use it!)

 It is is a very comprehensive but not excessively lengthy GitHub repo that will answer most of the questions you have ever had about, say, indenting when and case together — turns out they are supposed to be indented at the same level! (That means if I re-visit some earlier labs, cosmetic edits will need to be made.) The best part if, anyone is welcome to contribute and submit a pull request -- and maybe your take on comment indentation will be shared with the next generation of newbie developers.

Now, if there was only a website that did my Ruby code formatting for me...



