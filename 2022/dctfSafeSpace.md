### A python jail but hopefully the developer whitelisted enough tools for us to escape

This is a python jail that is somewhat restrictive. Though __ is filtered out from our py console. \__builtins__ is whitelisted and actually returns what normally would be \__builtins__.\__dict__.

![](./screenshots/dctf2022/builtinsFound.png)

The fact \__builtins__ is whitelisted makes me think this is the path the creator wants to steer us to. With these tools available maybe print(open(FILE).read()) would work to print the flag. Unfortunaty this is blocked we need a way to get around the blacklist of certain words but still run this payload. The interesting thing is that we have list available. We can use list(\__builtins__) to get the list version of the dict we can then specify an index to get the value at the index. Then we can get the actual function by using this value as the key to the \__builtins__ dict (remeber \__builtins__ == \__builtins__.\__dict__ in this jail). Allowing us to call open on \__builtins__'s FILE 

![](./screenshots/dctf2022/cleanSolution.png)

Yay, this challenge was pretty fun for me. Though I saw some people complaining about the arbitrarily nature of having \__builtins__ whitelisted and return \__builtins__.\__dict__ personally I feel like the intention was for it to be simpler for someone who has never encountered a python jail to pic up and solve. Me being one of thoose people I understand the appeal but also don't feel it was necessary. Instead of \__builtins__ specifically being allowed having __ not be blacklisted would have lead to more creativity though the most apparent solve would be the ineded way. It could also be because of infrastructure concerns it was so specific.
