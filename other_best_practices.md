# 50/72 rule
The 50/72 Rule is a set of standards that are pretty well agreed upon in the industry to standardize the format of commit messages. 50 is the maximum number of characters of the commit title, and 72 is the maximum character length of the commit body. These aren't arbitrary numbers that someone just pulled out of a hat.

An analysis of the commit messages in the linux kernel revealed that 50 characters is the most common length of a commit title. The number 72 comes from the fact that 80 characters is the widely accepted industry standard for readable character length of one line, git automatically adds a padding of 4 characters to the left of the commit message body, and to keep everything centered and looking nice, 4 characters should be padded to the right. Also, if an empty line separates the commit title from the body, git will automatically separate the two appropriately.

Origin: https://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html
And more discussions: https://stackoverflow.com/questions/2290016/git-commit-messages-50-72-formatting


# Technical debt:
https://devopedia.org/images/article/211/1799.1594111209.png

# SOLID principles:
Nice document describing with easy to understand illustrations:
https://medium.com/backticks-tildes/the-s-o-l-i-d-principles-in-pictures-b34ce2f1e898
