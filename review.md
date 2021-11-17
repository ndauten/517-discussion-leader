# Review

## Info

Reviewer Name: Senthil Rajasekaran
Paper Title: Certification of Programs for Secure Information Flow

## Summary

The paper presents a way of certifying programs with regard to secure infomration flow. The definition of "secure information flow" is one manufactured by the paper itself, and determining whether this is a reasonable concept is one of the key points of discussion regarding this work. The authors then go on to describe a computationally effecient way to compute this problem based on exploiting properties of lattices, which is followed by a short discussion of exceptional cases, practical applications, and weaknesses.

### Problem and why we care

The problem is based around making sure information is allowed to flow only in ways specified by a given security policy. This problem is fundamental to the idea of security, if low security objects are allowed to rewrite ones with high security then users with low security clearance will gain access to and potentially change confidential information. 

### Gap in current approaches
As far as I understand, this is an original direction. While there are other methods of certifying programs that were certainly around in 1977, none of them come close to being as fast as the lattice-based approach presented in this paper, which has a truly negligible runtime. The definition of certification also seems relatively new (with respect to the time period).

### Hypothesis, Key Idea, or Main Claim

The lattice based approach is an effective way to certify information flows in programs with respect to a security policy.

### Method for Proving the Claim

A brief implied argument about runtime complexity. The paper seems more concerned with presenting a novel idea rather than proving it. A theorem is also provided that proves a soundness type result for the presented program checker.

### Method for evaluating

A brief discussion about some applications. There's not much here.

### Contributions: what we take away

The method presented is a very nice idea and certainly significantly more effective than a naive approach. It remains to be determined if the problem solved is as robust as possible. The paper is overall quite excellent in my opinion and moderately well written. This approach is certainly one to remember.

## Pros (3-6 bullets)

The lattice based approach is fast.
It presents solutions to a variety of security concerns that existed before the paper - i.e. ones of individual importance.
The method is relatively easy to understand.

## Cons (3-6 bullets)
The paper is very short, and some important sections are skipped in lieu of extremely large figures.
The concept of "certification" used in this paper could have used more justification.
The "application" section offers almost nothing to the overall paper.


### What is your analysis of the proposed?

As stated before, I evaluate this paper as excellent. However, it has some troubles with presentation. It presents some extremely large figures and some useless sections when attention was needed in the following

1.)  Actually evaluating the runtime complexity, or at least the improvement over a naive approach. The authors merely state " It does not impair a program's execution
speed. " Well, what does the naive approach do? How about memory usage?
2.)  Justifying the concept of certification used.
3.)  If possible - proving this method optimal through some sort of lower bound.

However, the idea presented is simple but effective, making the paper clear to understand and a good addition to the literature. If I were reviewing this paper, I would like to give it around an 8/strong accept.

## Details Comments, Observations, Questions

The paper puts a mathematical frame around programs, which I appreciate a lot. As an example of an impossible guard specifying an information flow, the program if z == 0: if z == 1 : x := y (or something along those lines) is given. The idea is that this program still specifies a flow from y to x. However, the guard of this program is quite clearly busted in a very stupid way. What about a program like if (iHavePermission) : do (questionableAction). Does this still specify information flows? The program is literally asking for permission, and won't do something unless you let it! Yet it will still be uncertified due to the presence of the questionableAction.



