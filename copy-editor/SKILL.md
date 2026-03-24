---
name: copy-editor
description: Evidence-based copyediting for grammar, punctuation, usage, and consistency. Use when the user asks to copy edit, proofread, check grammar, or fix consistency errors in a document.
---

# COPY-EDITOR

**Purpose:** Catch mechanical errors in prose — grammar, punctuation, usage, consistency
**Approach:** Evidence-based (not prescriptivist, not permissivist)
**Inspired by:** Steven Pinker's *The Sense of Style* — especially the framework for evaluating disputed usage through evidence, logic, and historical awareness

---

## HOW TO USE

Say `/copy-editor` followed by a file path, or paste text directly:

```
/copy-editor path/to/chapter.md
```

Or: "Copy edit this chapter" / "Proofread this" / "Check this for grammar and consistency"

---

## WHAT THIS SKILL DOES

Runs three sequential passes on your prose:

| Pass | Focus | What It Catches |
|------|-------|----------------|
| **1. Usage** | Word-level correctness | Malaprop pairs, punctuation, it's/its, affect/effect, comma splices |
| **2. Grammar** | Sentence-level correctness | Subject-verb agreement, dangling modifiers, pronoun case errors |
| **3. Consistency** | Document-level consistency | Terminology variations, formatting inconsistencies, style drift |

---

## OUTPUT FORMAT

**CRITICAL: Always write the output to a file.** Do NOT print the annotated document into the conversation.

### File Output

If the input file is `chapter.md`, write the output to `chapter_copyedit.md` in the same directory.

The output file contains TWO sections:

**Section 1: Summary (at the top of the file)**

```markdown
## Copy Edit Summary

**Source:** [original filename]
**Date:** [date]

**Pass 1 (Usage):** N issues
**Pass 2 (Grammar):** N issues
**Pass 3 (Consistency):** N issues
**Total:** N issues found

### By Confidence
| Level | Count | Meaning |
|-------|-------|---------|
| HARD ERROR | N | Universally wrong — fix these |
| CONTESTED | N | Style guides disagree — your call |
| JUDGMENT | N | Context-dependent — consider both options |
```

**Section 2: Annotated Document (the full text with inline highlights)**

Reproduce the ENTIRE original document. For each issue, insert the annotation INLINE immediately after the flagged text, with everything inside brackets. Do NOT create paragraph breaks or change the document's structure.

Format: `==flagged text== [**CATEGORY** — Explanation. Suggested fix: "corrected text"]`

Everything — the category, the explanation, and the suggested fix — goes INSIDE the brackets. The annotation is part of the same paragraph as the flagged text. No line breaks between the highlight and the bracket.

Unflagged text is reproduced exactly as-is.

### After Writing the File

Tell the user:
1. Where the file was written
2. The total issue count
3. How many are hard errors vs. judgment calls

Open the file in Obsidian if available (`obsidian open file="filename" newtab`).

---

## PASS 1: USAGE

### Core Insight

Usage rules are neither logical necessities nor arbitrary inventions — they are **conventions that can be evaluated** through evidence, logic, and historical awareness.

### Usage Decision Tree

For every potential usage issue, follow this sequence:

```
1. IS THIS IN THE HARD ERROR TABLE?
   YES → Flag as ERROR | Confidence: HIGH
   NO  → Continue

2. IS THIS IN THE DISPUTED USAGE TABLE?
   YES → Flag as CONTESTED if it affects clarity
   NO  → Continue

3. IS THIS A ZOMBIE RULE?
   YES → DO NOT FLAG
   NO  → Continue

4. DOES IT AFFECT CLARITY OR MARK CARELESSNESS?
   YES → Flag as USAGE | Confidence: MEDIUM
   NO  → DO NOT FLAG (avoid peevology)
```

When uncertain, label `LOOKUP: defer to style guide` rather than inventing certainty.

---

### Hard Errors (Always Flag — HIGH Confidence)

| Error | Example Wrong | Example Correct | Test |
|-------|---------------|-----------------|------|
| **affect/effect** | "The law effects everyone" | "The law affects everyone" | verb=influence: affect; noun=result: effect |
| **it's/its** | "The dog wagged it's tail" | "The dog wagged its tail" | Can you expand to "it is"? |
| **who's/whose** | "Who's book is this?" | "Whose book is this?" | Can you expand to "who is"? |
| **lose/loose** | "Don't loose your keys" | "Don't lose your keys" | lose=misplace; loose=not tight |
| **lie/lay** | "Lay down and rest" | "Lie down and rest" | Direct object? Yes: lay; No: lie |
| **dangling modifier** | "Walking to the store, the rain started" | "Walking to the store, I got wet" | Does implied agent match subject? |
| **apostrophe for plural** | "The Smith's are coming" | "The Smiths are coming" | Never apostrophe for plural |
| **comma splice** (formal) | "It was late, I left" | "It was late, so I left" | Two independent clauses need more than comma |
| **malaprop confusions** | See full table below | — | Check against malaprop pairs |

---

### Disputed Usage (Context-Dependent — CONTESTED)

These constructions are contested. Flag only when the choice affects clarity or consistency.

| Construction | Traditional View | Modern Reality | Recommendation | When to Allow Exception |
|--------------|------------------|----------------|----------------|-------------------------|
| **data is/are** | Plural only | Singular standard | Accept singular | Always acceptable |
| **hopefully** (sentence adverb) | "Wrong" | Fully legitimate | Accept | Always acceptable |
| **literally** (hyperbolic) | "Misuse" | Centuries old | Accept (informal) | Flag only in formal/precise contexts |
| **which** in integrated clauses | Use "that" | British: "which" OK | Prefer "that" | Note pattern; don't flag every instance |
| **split infinitives** | "Never split" | Split when natural | Accept | Always acceptable |
| **preposition at end** | "Never end with" | Fine | Accept | Always acceptable |
| **none is/are** | Singular only | Both correct | Accept both | Choose based on meaning |
| **between** (3+ items) | "Among" for 3+ | OK for 1-to-1 relations | Accept | "Between the three nations" is correct |
| **less/fewer** | fewer=count, less=mass | Some idioms cross | Prefer distinction | Accept "less than 10 people" |
| **who/whom** | Object=whom | Fading in speech | Require in formal | Accept "who" informally |
| **singular they** | "Error" | Established | Accept | Preferred for gender-neutral |
| **comprise/composed** | "Whole comprises parts" | "Is comprised of" OK | Accept both | Don't hypercorrect |

---

### Zombie Rules (NEVER Flag)

These "rules" have no basis. **Do not flag. Do not enforce.**

| "Rule" | Origin | Why It's Bogus |
|--------|--------|----------------|
| Don't split infinitives | 19th c. Latinizers | English is not Latin; split when natural |
| Don't end with preposition | Dryden's preference | Used by best writers for centuries |
| Don't begin with And/But | School teacher myth | Common in great literature |
| "Hopefully" is wrong | 1960s prescriptivists | Like "frankly," "sadly" — long-established |
| "None" always singular | False etymology | Can mean "not one" OR "not any" |
| "Data" always plural | Latin rule | English treats it as singular |
| "They" can't be singular | 18th c. grammarians | Shakespeare, Austen, modern usage |

### Bogus Distinctions (DO NOT FLAG as errors)

These "distinctions" are not observed by careful writers:

| "Rule" | Reality |
|--------|---------|
| aggravate = only "make worse" | "Irritate" sense has long history |
| anticipate = only "prepare for" | Both senses legitimate |
| anxious = only "worried" | "Eager" sense has centuries of use |
| begs the question = only "circular reasoning" | "Raises the question" sense is now dominant |
| comprise: "whole comprises parts" only | "Is comprised of" is established |
| crescendo = only "buildup" | "Peak" sense is standard |
| critique = noun only | Verb use is established |
| data = always plural | Singular use is common in modern English |
| decimate = only "kill one in ten" | "Devastate" sense is universal |
| dilemma = only two choices | Broader sense is standard |
| disinterested = only "impartial" | "Uninterested" sense has long history |
| enormity = only "wickedness" | "Enormousness" sense is established |
| fortuitous = only "by chance" | "Fortunate" sense is common |
| fulsome = only "excessive/insincere" | "Full/abundant" is the original sense |
| I could care less | Illogical but idiomatic; "couldn't" is safer |
| irregardless | Nonstandard; use "regardless" **(EXCEPTION: do flag this one)** |
| literally = only literal | Hyperbolic use is centuries old |
| nauseous = only "causing nausea" | "Nauseated" sense is standard |
| parameter = only technical | Broader sense is established |
| protagonist = only one per story | Multiple protagonists is fine |

---

### Confidence Levels

| Level | Meaning | Action |
|-------|---------|--------|
| **HIGH** | Objective error; no reasonable dispute | Flag always; suggest fix |
| **MEDIUM** | Judgment call; depends on context/style | Flag with rationale; offer alternative |
| **LOW** | Uncertain; may be style-dependent | Label `LOOKUP: check style guide` |

**Rule:** When confidence is LOW, label rather than assert. Never invent certainty.

---

### Malaprop Pairs Checklist

Flag any confusion between these commonly mixed words:

**High-Frequency Confusions:**

| Word 1 | Word 2 | Distinction |
|--------|--------|-------------|
| **affect** (verb) | **effect** (noun) | influence vs. result |
| **lie** (recline) | **lay** (put down) | no object vs. needs object |
| **it's** | **its** | contraction vs. possessive |
| **who** | **whom** | subject vs. object |
| **that** | **which** | integrated vs. supplementary clause |

**Full Malaprop Table:**

| Correct | Confused With | Distinction |
|---------|---------------|-------------|
| adverse | averse | unfavorable vs. reluctant |
| allusion | illusion | indirect reference vs. false perception |
| appraise | apprise | assess value vs. inform |
| born | borne | brought to life vs. carried |
| censor | censure | suppress vs. criticize |
| chord | cord | musical notes vs. string |
| climactic | climatic | relating to climax vs. climate |
| complementary | complimentary | completing vs. praising/free |
| credible | credulous | believable vs. gullible |
| criteria | criterion | plural vs. singular |
| discreet | discrete | tactful vs. separate |
| emigrate | immigrate | leave country vs. enter country |
| eminent | imminent | distinguished vs. about to happen |
| flaunt | flout | show off vs. defy |
| flounder | founder | struggle vs. sink/fail |
| gibe | jibe | taunt vs. agree |
| grisly | grizzly | gruesome vs. gray/bear |
| hone | home in | sharpen vs. zero in |
| imply | infer | suggest vs. conclude |
| loath | loathe | reluctant vs. hate |
| lose | loose | misplace vs. not tight |
| luxuriant | luxurious | lush growth vs. rich comfort |
| militate | mitigate | work against vs. lessen |
| ordinance | ordnance | law vs. weapons |
| palate | palette | taste/mouth vs. artist's board |
| pedal | peddle | foot lever vs. sell |
| peak | peek/pique | summit vs. glance/stimulate |
| prescribe | proscribe | recommend vs. forbid |
| principal | principle | main person vs. rule |
| reticent | reluctant | uncommunicative vs. unwilling |
| staunch | stanch | loyal vs. stop bleeding |
| tortuous | torturous | winding vs. painful |
| turbid | turgid | muddy vs. swollen/pompous |
| unexceptional | unexceptionable | ordinary vs. unobjectionable |
| venal | venial | corrupt vs. forgivable |

---

### Affect/Effect Special Check

The most common confusion:

| Form | Usage | Example |
|------|-------|---------|
| **affect** (verb) | to influence | "The weather affects my mood" |
| **effect** (noun) | a result | "The effect was dramatic" |
| **effect** (verb) | to bring about (formal) | "She effected change" |
| **affect** (noun) | emotion display (psych) | "Flat affect" |

For every instance of affect/effect, verify correct part of speech.

---

### Lie/Lay Special Check

The confusion arises because past tense of "lie" = "lay":

| Verb | Meaning | Present | Past | Past Participle |
|------|---------|---------|------|-----------------|
| **lie** | recline | lie | lay | lain |
| **lay** | put down | lay | laid | laid |

**Test:** Is there a direct object? Object → lay. No object → lie.

Common errors:
- "Lay down and rest" → "Lie down and rest"
- "I laid in bed" → "I lay in bed"

---

### It's/Its Check

Possessive pronouns never have apostrophes.

| Form | Meaning | Test |
|------|---------|------|
| **it's** | it is / it has | Can you expand it? |
| **its** | possessive | Like "his" or "hers" |

---

### Apostrophe Audit

| Use | Rule | Example |
|-----|------|---------|
| Possession | Add 's (or ' for plurals ending in s) | "The dog's leash" |
| Contractions | Marks omitted letters | "don't" |
| **NEVER** plurals | Never use apostrophe for plural | "The 1990s" NOT "1990's" |

---

### Comma Checklist

**Comma Splice (ERROR):**
- **Wrong:** "It was late, I went home"
- **Right:** "It was late, so I went home" / "It was late; I went home"
- **Exception:** Very short parallel clauses ("I came, I saw, I conquered")

**Restrictive vs. Nonrestrictive:**

| Type | Commas? | Example |
|------|---------|---------|
| Integrated (restrictive) | No commas | "The car that I bought is blue" |
| Supplementary (nonrestrictive) | Commas | "The car, which I bought, is blue" |

**Test:** Remove the clause. If the sentence still works, use commas.

**Serial Comma:** Include it ("red, white, and blue"). Prevents ambiguity.

---

### Who/Whom Check

**Rule:** Who = subject; Whom = object.
**Test:** Substitute he/him in the relative clause. "He" → who. "Him" → whom.

- "The man who called" (he called)
- "The man whom I called" (I called him)
- "Who do you think will win?" (you think HE will win → who)

**Trap:** Don't be misled by intervening phrases. What matters is the function in the relative clause.

---

### That/Which Check

| Use | For | Example |
|-----|-----|---------|
| **that** | Integrated (restrictive) clauses | "The book that I read" |
| **which** | Supplementary (nonrestrictive) clauses | "The book, which I enjoyed, is here" |

**Test:** Can you remove the clause without losing identity of the referent? Yes → "which" + commas. No → "that" (no commas).

---

### Less vs. Fewer

| Use | For | Example |
|-----|-----|---------|
| **fewer** | count nouns | "Fewer books" |
| **less** | mass nouns | "Less water" |

Accepted exceptions: "less than twenty people," "less than five miles," "one less thing to worry about." Don't hypercorrect established idioms.

---

### Conditionals and Subjunctive

| Condition Type | Form | Example |
|----------------|------|---------|
| **Open condition** (may be true) | Indicative | "If she was here yesterday, I didn't see her" |
| **Counterfactual** (known false) | Subjunctive "were" | "If she were here now, she would help" |
| **Remote condition** (unlikely) | Either acceptable | "If I was/were rich, I'd travel" |

Use "were" for conditions the speaker knows to be false. After "wish," prefer subjunctive: "I wish I were taller."

---

### Flat Adverbs

"Drive slow" vs. "Drive slowly" — is the form without -ly an error?

**No.** Flat adverbs are grammatically legitimate.

| Status | Examples |
|--------|----------|
| ACCEPT | "Drive slow," "Go direct," "Hold tight," "Stand firm" |
| ACCEPT | "She looked directly at him" (when -ly is natural) |
| REQUIRED FLAT | "She held him close" (not "closely") |

**DO NOT FLAG** flat adverbs that sound natural.

---

### Fused Participle

"I appreciate you helping me" vs. "I appreciate your helping me"

Both are acceptable. The "rule" requiring possessives before gerunds is a zombie.

| Form | When Natural |
|------|--------------|
| "I appreciate you helping" | When the agent matters |
| "I appreciate your helping" | When nominalizing the action |
| "the chance of that happening" | Fused form often required |
| "people making assumptions" | Fused form necessary (not "people's making") |

**DO NOT FLAG** fused participles as errors.

---

### Absolute Adjectives

Can you say "very unique" or "more perfect"?

| Context | Handling |
|---------|----------|
| Formal/precise writing | Respect absolute meaning; flag "very unique" |
| Casual contexts | Modification widely accepted |
| Established phrases | "A more perfect Union" has centuries of use |

Flag as CONTESTED in formal contexts, not HARD ERROR.

---

### Quotation Marks and Punctuation

**American vs. British:**

| Issue | American | British |
|-------|----------|---------|
| Commas/periods | **Inside quotes** | Logical placement |
| Colons/semicolons | Outside quotes | Outside quotes |
| Question/exclamation marks | Logical placement | Logical placement |

**American Rule (default):** Commas and periods always go inside closing quotation marks.

**Exception:** When precision matters (code, philosophy).

Follow house style (American or British). Don't mix systems within a document.

---

### Intellectual Standards for Usage

When evaluating any usage question, apply:

1. **Intellectual humility** — Many confident pronouncements are wrong
2. **Historical awareness** — Know where rules come from
3. **Evidence-based reasoning** — Check what good writers actually do
4. **Appreciation of language change** — English evolves; that's not decay
5. **Resistance to peevology** — Don't enforce rules just to feel superior
6. **Focus on real clarity** — Energy spent on bogus rules is wasted

**The ultimate test:** Does the convention serve communication, or does it serve gatekeeping?

---

## PASS 2: GRAMMAR

### Core Insight

**Tree-blindness:** Writers lose track of phrase structure while converting their mental tree into a linear string of words. This causes agreement errors, dangling modifiers, and case errors.

---

### Subject-Verb Agreement

**The trap:** A nearby noun "hijacks" agreement from the true subject.

```
WRONG:  "The impact of the cuts have not been felt yet."
                       ^^^^            ^^^^
                   hijacker         wrong verb

RIGHT:  "The impact of the cuts has not been felt yet."
```

**Audit steps:**
1. Find every verb
2. Trace back through the tree to the true subject
3. Ignore intervening nouns
4. Verify number agreement

**Phrases that don't change subject number:** "as well as," "along with," "together with," "including," "in addition to."

Example: "The president, along with the cabinet, IS meeting" (not "are").

### Neither/Nor and Either/Or Agreement

The verb agrees with the **nearest subject:**

| Construction | Nearest Subject | Verb |
|--------------|-----------------|------|
| "Neither the manager nor the employees" | employees (plural) | were |
| "Neither the employees nor the manager" | manager (singular) | was |
| "Either the students or the teacher" | teacher (singular) | is |
| "Either the teacher or the students" | students (plural) | are |

### Special Cases

| Structure | Agreement |
|-----------|-----------|
| "There is/are" | Agrees with what follows ("There are many reasons") |
| "One of the [plural] who" | Relative verb agrees with plural ("One of the men who ARE") |
| "Each/Every" | Always singular ("Every one of the books IS") |
| "None" | Singular or plural depending on meaning |

### Collective Nouns

| Noun | British | American |
|------|---------|----------|
| Team, committee, family | Often plural | Usually singular |
| Data | Plural | Increasingly singular |
| Media | Plural | Increasingly singular |

Flag as CONTESTED — note both options.

---

### Dangling Modifiers

A participial phrase must have its implied subject match the grammatical subject of the main clause.

```
WRONG:  "Driving to the airport, the radio reported severe delays."
RIGHT:  "Driving to the airport, I heard the radio report severe delays."
```

**Audit:** For every sentence beginning with an -ing phrase, -ed phrase, or infinitive phrase — check: does the subject of the main clause match the implied agent?

| Wrong | Right |
|-------|-------|
| "Born in Brooklyn, his formative years were spent in Queens." | "Born in Brooklyn, he spent his formative years in Queens." |
| "Turning the corner, the view was magnificent." | "Turning the corner, I saw a magnificent view." |
| "Having studied the problem, a solution emerged." | "Having studied the problem, we found a solution." |

**Acceptable Absolute Participles (DO NOT FLAG):**
- "Considering the circumstances..."
- "Speaking of which..."
- "Broadly speaking..."
- "Given that..."
- "Judging from..."
- "Assuming that..."

---

### Pronoun Case

| Function | Case | Forms |
|----------|------|-------|
| Subject | Nominative | I, he, she, we, they, who |
| Object | Accusative | me, him, her, us, them, whom |

**Common Errors:**

**Hypercorrection after preposition:**
- **Wrong:** "Between you and I"
- **Right:** "Between you and me"

**Coordination test:** Try each pronoun alone. "Give it to John and [me/I]" → "Give it to me" → "Give it to John and me."

**After "than" or "as":** Depends on implied verb.
- "She's taller than I [am]" — nominative
- "This affects you more than [it affects] me" — accusative

### Who/Whom

**Test:** Substitute he/him:
- "Who did this?" → "He did this" → WHO
- "Whom should I call?" → "I should call him" → WHOM

**The trap:** Intervening phrases mislead. "The candidate who I think will win" — "who" is correct (subject of "will win," not object of "I think").

**Note:** "Whom" is fading from English. In informal contexts, "who" for object is increasingly acceptable. Flag as CONTESTED in informal writing.

---

### Parallelism

Items in a list or comparison must match in grammatical form.

```
WRONG:  "She likes hiking, swimming, and to ride bikes."
RIGHT:  "She likes hiking, swimming, and riding bikes."
```

---

## PASS 3: CONSISTENCY

### Purpose

This pass ensures the document is internally consistent. Even when multiple forms are acceptable, a document should pick one and stick with it.

---

### Terminology Consistency

**Same concept = same term throughout.**

Track:
1. **Technical terms** — "time-line" vs. "timeline" vs. "time line" — pick one
2. **Proper nouns** — Consistent capitalization and spelling (people's names especially)
3. **Abbreviations** — Define on first use, use consistently after
4. **Concept labels** — If you call it "the framework" in Chapter 1, don't call it "the model" in Chapter 5

**Audit process:**
1. Build terminology list as you read
2. Flag variations when they appear
3. Note which form appears first (usually becomes the standard)
4. Let author decide which form to standardize on

---

### Formatting Consistency

**Numbers:**

| Context | Style A | Style B | Rule |
|---------|---------|---------|------|
| Small numbers | "three" | "3" | Pick one threshold (usually 10) |
| Large numbers | "1,000" | "1000" | Pick one separator style |
| Percentages | "50 percent" | "50%" | Pick one |
| Dates | "January 15, 2026" | "15 January 2026" | Pick one format |

**Lists:** Parallel structure, consistent punctuation, consistent capitalization.

**Headings:** Title Case vs. Sentence case — pick one. Periods or no periods — pick one.

**Punctuation patterns:**

| Pattern | Style A | Style B |
|---------|---------|---------|
| Serial comma | "A, B, and C" | "A, B and C" |
| Quotation marks | "double" | 'single' |
| Em dashes | "word—word" | "word — word" |
| Ellipses | "..." | ". . ." |

---

### Style Guide Adherence

**If author specifies a style guide:** Check against that guide (Chicago, AP, APA, house style).

**If no style guide specified:** Use internal consistency as the standard. Note the author's patterns. Flag deviations from those patterns. Don't impose external rules.

**Common style guide differences:**

| Issue | Chicago | AP |
|-------|---------|-----|
| Serial comma | Yes | No |
| Numbers | Spell out 1-100 | Spell out 1-9 |
| Titles | Italics for books | Quotes for books |
| "Percent" | Spell out | Use % |

---

### Cross-Reference Consistency

**Internal references:**
- "See Chapter 3" — Does Chapter 3 exist?
- "As discussed above" — Was it actually discussed?
- "In the next section" — Is there a next section?

**Figure/Table references:**
- "Figure 1 shows..." — Does Figure 1 exist?
- Are figures numbered sequentially?

**Citation consistency:** Same format throughout. All cited works in bibliography. All bibliography entries cited in text.

---

### Consistency Audit Checklist

**First pass — Build inventory:** Track first occurrence of key terms, proper nouns, abbreviations, number formatting, list formatting, heading styles.

**Second pass — Flag inconsistencies:** For each item in inventory, find all occurrences, flag variations, note locations.

**Third pass — Cross-references:** Verify all internal references, figure/table references, citation consistency.

---

## WHAT THIS SKILL DOES NOT DO

- **Voice decisions** — This skill won't rewrite your sentences for style or clarity
- **Restructuring** — It won't reorganize paragraphs or arguments
- **Fact-checking** — It flags potential factual issues but doesn't verify them
- **Creative judgment** — Intentional rule-breaking is preserved. If it looks deliberate, it's noted but not flagged as an error

---

## PRINCIPLES

1. **Evidence over authority** — Usage rules are conventions that can be evaluated, not commandments
2. **Never enforce zombie rules** — Don't flag split infinitives, sentence-ending prepositions, or singular they
3. **Confidence levels matter** — Hard errors get flagged with certainty. Contested usage gets flagged with options. Judgment calls get flagged with both sides
4. **Preserve the author's voice** — Copyediting fixes mechanics. It does not change how the author sounds
5. **When uncertain, say so** — Label uncertainty rather than inventing confidence

*"The answer to most disputed usage questions is 'Look it up.' But look it up in a modern usage guide that bases its recommendations on evidence." — Steven Pinker, The Sense of Style*
