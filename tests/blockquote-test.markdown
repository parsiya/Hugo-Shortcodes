---

date: 2016-04-16T00:07:14-04:00
draft: false
title: Blockquote test
---

Normal quote:
{{< blockquote >}}
  This is a simple quote.
{{< /blockquote >}}

Quote with author
{{< blockquote author="Author2" >}}
  This is a quote with only an Author named Author2.
{{< /blockquote >}}

Quote with author and source
{{< blockquote author="Author3" source="Source" >}}
  This is a quote from Author3 and source "source."
{{< /blockquote >}}

Quote with author and link
{{< blockquote author="Author4" link="https://www.google.com" >}}
  This is a quote from Author4 and links to https://www.google.com.
{{< /blockquote >}}

Quote with author, link and title
{{< blockquote author="Author5" link="https://www.google.com" title="Google" >}}
  This is a quote from Author5 and links to https://www.google.com with title "Google."
{{< /blockquote >}}

Quote with author and a link longer than 32 characters, string is first cut at 32 characters then everything after the last forward slash is removed
{{< blockquote author="Author6" link="https://twitter.com/CryptoGangsta/status/716427930126196737" >}}
  This is a quote from Author5 and links to https://twitter.com/CryptoGangsta/status/716427930126196737 which is longer than 32 characters.
  <br>And this is a new line in the quote with the HTML br tag.
{{< /blockquote >}}

Test from the Octopress blockquote page at: http://octopress.org/docs/plugins/blockquote/
{{< blockquote author="@allanbranch" link="https://twitter.com/allanbranch/status/90766146063712256" >}}
  Over the past 24 hours I've been reflecting on my life & I've realized only one thing. I need a medieval battle axe.
{{< /blockquote >}}

Long multiline quote:
{{< blockquote author="Paul Graham" title="Write Like You Talk" link="http://www.paulgraham.com/talk.html" >}}
Here's a simple trick for getting more people to read what you write: write in spoken language.

Something comes over most people when they start writing. They write in a different language than they'd use if they were talking to a friend. The sentence structure and even the words are different. No one uses "pen" as a verb in spoken English. You'd feel like an idiot using "pen" instead of "write" in a conversation with a friend.

<...>

You don't need complex sentences to express complex ideas. When specialists in some abstruse topic talk to one another about ideas in their field, they don't use sentences any more complex than they do when talking about what to have for lunch. They use different words, certainly. But even those they use no more than necessary. And in my experience, the harder the subject, the more informally experts speak. Partly, I think, because they have less to prove, and partly because the harder the ideas you're talking about, the less you can afford to let language get in the way.

<...>

People often tell me how much my essays sound like me talking. The fact that this seems worthy of comment shows how rarely people manage to write in spoken language. Otherwise everyone's writing would sound like them talking.

If you simply manage to write in spoken language, you'll be ahead of 95% of writers. And it's so easy to do: just don't let a sentence through unless it's the way you'd say it to a friend.
{{< /blockquote >}}

Quote with title and no link
{{< blockquote author="Author5"  title="Google" >}}
  This is a quote from Author5 and links to https://www.google.com with title "Google."
{{< /blockquote >}}

<!--more-->
