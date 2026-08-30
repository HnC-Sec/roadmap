---
date: '2026-08-30T00:00:00Z'
draft: false
title: 'Intermediate Research and Learning'
weight: 100
topics:
  - Finding deeper resources
  - Synthesizing knowledge
  - Finding and reading academic research
milestones:
  - Find and understand academic research
  - Infer details from incomplete data
  - Research deeper learning techniques independently
knowledge_check:
  - Metasearch engine
  - Search operators
  - Boolean queries
  - Professional Networking
certifications:
  - None
learning_resources:
  - title: "Infocon"
    cost: "Free"
    time: "Varies"
    url: "https://infocon.org/"
    link_text: "Infocon.org"
    notes: "Community supported, non-commercial archive of all the past hacking and infosec related conference and convention material that can be found."
  - title: "How to Read a Paper"
    cost: "Free"
    time: "20 Minutes"
    url: "https://web.stanford.edu/class/ee384m/Handouts/HowtoReadPaper.pdf"
    link_text: "Stanford (PDF)"
    notes: "S. Keshav's three-pass method for reading academic papers efficiently. Short, and worth re-reading."
  - title: "Google Scholar"
    cost: "Free"
    time: "Varies"
    url: "https://scholar.google.com"
    link_text: "Google Scholar"
    notes: "Search engine limited to scholarly, peer-reviewed sources. Use the 'Cited by' link to walk forward in time from a paper."
  - title: "arXiv"
    cost: "Free"
    time: "Varies"
    url: "https://arxiv.org"
    link_text: "arXiv"
    notes: "Preprint archive. Papers here are often not yet peer reviewed, so read them with extra care."
  - title: "USENIX Security Proceedings"
    cost: "Free"
    time: "Varies"
    url: "https://www.usenix.org/publications/proceedings"
    link_text: "USENIX"
    notes: "Open-access proceedings from a top security conference. A good place to see what real security research looks like."
  - title: "Semantic Scholar"
    cost: "Free"
    time: "Varies"
    url: "https://www.semanticscholar.org"
    link_text: "Semantic Scholar"
    notes: "Academic search with citation graphs and auto-generated summaries. Useful for mapping a field you are new to."
  - title: "Connected Papers"
    cost: "Free (limited) / $6 per month"
    time: "30 Minutes"
    url: "https://www.connectedpapers.com"
    link_text: "Connected Papers"
    notes: "Builds a visual graph of papers related to one you already have. Fast way to find the neighbours of a paper."
  - title: "Learning How to Learn"
    cost: "Free to audit / $49 certificate"
    time: "~15 Hours"
    url: "https://www.coursera.org/learn/learning-how-to-learn"
    link_text: "Coursera"
    notes: "Barbara Oakley's course on spaced repetition, chunking, and beating procrastination."
  - title: "A Mind for Numbers"
    cost: "~$15"
    time: "~8 Hours"
    url: "https://barbaraoakley.com/books/a-mind-for-numbers/"
    link_text: "Barbara Oakley"
    notes: "The book version of the course above, with more depth on technical study habits."
  - title: "Google Advanced Search Operators"
    cost: "Free"
    time: "30 Minutes"
    url: "https://ahrefs.com/blog/google-advanced-search-operators/"
    link_text: "Ahrefs"
    notes: "Practical reference for site:, filetype:, intitle:, and the rest."
---

In the Basic Research and Learning section you learned how to find sources and judge whether they can be trusted. That works well while you are studying subjects that many people have already written about. At some point you will run into a question where the good sources run out: a protocol nobody has documented well, a bug that only three people on the internet have seen, or a technique that is only a year old. This section is about what to do then.

The short version: you stop looking for an answer, and start assembling one.

## Searching Deliberately

Most people type a few words into a search box and take what comes back. You can do much better by treating a search as something you design.

**Search operators** are special keywords a search engine understands. They narrow results in ways that ordinary words cannot. The most useful ones are:

- `site:example.com` — only return results from one site. Good for searching a vendor's documentation when their own search is bad.
- `filetype:pdf` — only return one file type. Useful for finding whitepapers, manuals, and specifications.
- `intitle:` and `inurl:` — the words must appear in the page title or the URL.
- `"exact phrase"` — quotation marks force an exact match, which matters a lot for error messages.
- `-word` — exclude results containing a word. Useful for cutting out a popular topic that shares a name with yours.

**Boolean queries** combine your terms with logic: `AND` means both must appear, `OR` means either will do, and brackets group them. A query like `("port knocking" OR "single packet authorization") AND firewall` finds pages about a concept even when different authors give it different names.

A **metasearch engine** runs your query against several search engines at once and merges the results. [SearXNG](https://searx.be) is a common open-source example. These are useful because every search engine ranks and filters differently, so a page that is buried on one may be near the top of another.

Also change the words themselves, not just the operators. Vendors, academics, and practitioners often describe the same idea with different vocabulary. "Lateral movement", "east-west traffic", and "pivoting" can all point at the same behaviour. If a search is going nowhere, the term you are using may simply not be the one your sources use.

## Finding and Reading Academic Research

Academic papers are where a lot of security knowledge appears first, often years before it shows up in a blog post or a product. They are also intimidating, mostly because people try to read them like a book. Don't.

Use a **three-pass approach**:

1. **First pass (5–10 minutes).** Read the title, abstract, introduction, section headings, and conclusion. Skip everything else. At the end you should be able to say what the paper claims and whether it is relevant to you. Many papers stop here, and that is fine.
2. **Second pass (about an hour).** Read the body, but ignore proofs and heavy maths. Look closely at figures, tables, and graphs — they usually carry the real result. Note references you want to follow.
3. **Third pass (several hours).** Only for papers you need to fully trust or reproduce. Work through the details as though you were re-doing the work yourself, and challenge every assumption.

A few things to know about where papers live. **Peer review** means other experts in the field checked the work before publication; it raises confidence but does not guarantee correctness. A **preprint** (such as most of what is on arXiv) has not been through that process yet. **Open access** means the paper is free to read; a great deal of security research is open access, including the proceedings of major conferences such as USENIX Security, IEEE S&P, ACM CCS, and NDSS. If you hit a paywall, check the authors' own university pages — researchers very often host a free copy of their own work.

Two navigation tricks are worth building into your habits. Following a paper's **references** walks you backwards to the work it was built on, which is how you find the foundational papers in a field. Following its **citations** (Google Scholar's "Cited by" link) walks you forwards to newer work that used it, which is how you find out whether its conclusions still hold.

## Synthesizing Knowledge

Synthesis is the skill of building an understanding out of pieces that no single source gives you. It is what separates someone who can only apply documented answers from someone who can work on new problems.

In practice it looks like this. You have a vendor datasheet that describes half of a protocol, a packet capture that shows behaviour the datasheet doesn't mention, a ten-year-old forum post from someone who hit the same thing, and the source code of a client that talks to it. None of those is an answer. Read together, they let you form a model of how the thing works — and then you test that model.

Some habits that make this work:

- **Write down what you believe, and mark how sure you are.** Separating "the docs state this", "I observed this", and "I am guessing this" keeps you from building on a guess without noticing.
- **Look for agreement across independent sources.** Two sources agreeing means little if one copied the other. Ask where each author actually got their information.
- **Prefer primary sources.** The RFC, the specification, the source code, or your own packet capture beats a blog post summarizing them. Blog posts are useful for orientation, not for final answers.
- **Test your model.** The point of inferring something is that it makes a prediction. Set up a small experiment and check whether the prediction holds. In security work, being confidently wrong is expensive.
- **Record the gaps.** Noting "I still don't know how it handles a session timeout" gives you a list of things to attack next, rather than a vague feeling that something is missing.

## Learning From People

Not everything is written down. Some knowledge only exists in the heads of people who do the work, and the way to reach it is **professional networking** — building genuine working relationships with other people in your field.

This is far less formal than the phrase suggests. It mostly means being present and useful in places where practitioners talk: community Discord and Matrix servers, mailing lists, local meetups and conference hallways, and open-source project issue trackers. Answer questions when you can. Publish your own writeups and notes; being visibly useful is what gets people to answer *you* later. Ask specific questions rather than general ones — the same rules from the basic section still apply, and they matter more when you are asking for someone's time.

Two cautions. First, treat what you are told the same way you treat any other source: an experienced person can still be out of date or simply wrong, and "someone in a Discord said so" is not evidence. Second, take the same care with what you share. In security, details about systems, tools, and unpublished findings can be sensitive, and a friendly conversation is a well-known route for gathering them.

## Directing Your Own Learning

By this point you should be choosing what to learn, not just how. That means occasionally stepping back and asking what you are actually trying to become good at, then working backwards to the topics that serve it. It also means noticing when a method has stopped working for you and going to find a better one — there is a large body of research on spaced repetition, retrieval practice, and interleaving, and those techniques are themselves a subject you can go and research using everything above.

The final marker of this level is a comfortable one: when you meet an unfamiliar topic, you no longer wonder whether you can learn it. You just start.
