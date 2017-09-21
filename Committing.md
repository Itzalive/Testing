# Committing
## Summary
 1. Separate subject from body with a blank line
 2. Limit the subject line to 50 characters
 3. Capitalize the subject line
 4. Do not end the subject line with a period
 5. Use the imperative mood in the subject line
 6. Wrap the body at 72 characters
 7. Use the body to explain what and why vs. how
 8. Each commit should change a single thing
## Example
```
Short (50 chars or less) summary of changes

More detailed explanatory text, if necessary. Wrap it to about y entirely); tools like rebase can get
confused if you run the two together.

Explain the problem that this commit is solving. Focus on why you
are making this change as opposed to how (the code explains that).
Are there side effects or other unintuitive consequences of this
change? Here's the place to explain them. 

Further paragraphs come after blank lines.

  - Bullet points are okay, too

  - Typically a hyphen or asterisk is used for the bullet, preceded
    by a single space, with blank lines in between

With the issue tracker, put references to them at the bottom and they
will be linked automatically. If you have completed an issue you can
use ‘closes’, ‘fixes’ or ‘resolves’. Like this:

resolves #123
fixes #57
See also #456, #789
```

## Detail
 1. The first line should always be a summary (typically 50 characters or less) and that it should be followed by a blank line.
 2. Don't end the summary line with a period - it's a title and titles don't end with a period. Also capitalise it.
 3. The commit message is a description of what the commit does and not what you have done and write it like it is a command - ‘add’, ‘fix’, ‘change’ etc. not ‘added’, ‘fixed’, ‘changed’. (Imagine it is always prefixed by “If applied, this commit will…”)
 4. Each commit should be changing one thing, commits should be atomic. This is so that commits can be reverted without having to change anything else. A branch for a feature should contain a lot of commits as each part of the feature is added. Not a single commit for “Adding feature”. If you find yourself writing “Add this and that” it should probably be more than one commit.
 5. The commit message should have enough information to say what the commit does and why without looking at the file changes. You don’t need to include how it does those things because the code shows that.
 6. Each commit should answer the following questions. If you can do this in the summary then that is ok.  
    1. **Why is this change necessary?**  
    This question tells code reviewers of your pull request what to expect in the commit, allowing them to more easily identify and point out unrelated changes.
  
    2. **How does it address the issue?**  
    Describe, at a high level, what was done to affect change.  
     If your change is obvious, you may be able to omit addressing this question.
    3. **What side effects does this change have?**  
    This is the most important question to answer, as it can point out problems where you are making too many changes in one commit or branch. One or two bullet points for related changes may be okay, but five or six are likely indicators of a commit that is doing too many things. 

 7. If a commit links to a specific task or issue then it should link to it (in both directions)
 8. If you are fixing a bug, your commit message (or the linked task) should include steps to replicate the bug (before the commit) so a code reviewer can check the commit fixes the issue. If a bug cannot be replicated there needs to be a more detailed explanation of why the changes made will fix the issue.
 9. If you make a mistake say what the mistake was not that it was a mistake. “Fix missing files from XYZ project”, “Fix typo in XYZ”, “Fix namespace issues after restructure”

## Examples of bad commit messages and why:
*“Correcting for my stupidity!” - GG*
 - Correcting what?
 - Why?

*“Tried to make a test showing why Sinéad's script wasn't working... test passed first time so need to keep investigating. Still a useful test” - EH*
 - This is saying what you have done not what the commit does. It may be relevant information but there is a lot of information missing.
 - A better summary would be “Added a new test script for …”
 - Should include:
   - Why wasn’t Sinead’s script working?
   - What is the new test supposed to test?
   - How does this test achieve that?
   - Why did it pass if you didn’t expect it to? Does it test what you meant to test? Is the reason Sinead’s script didn’t work wrong?

*“Changes and additions to benchmarking” – BQ*
 - Change/s/ suggests this could have been separate commits
 - What changes and why?
 - What additions?

*“Updates to tests” – EH*
 - What updates?
 - Which tests?
 - Why?

*“Fix broken tests, still avoiding tedious manual casting.” - RA*
 - What tests?
 - Why were they broken?
 - How were they fixed?

*“Commiting changes to the simulator refactor branch” – DE*
 - What changes?
 - Why?
 - Wrong tense for summary it is too personal.

*“Slight Mod based on feedback from Adrian” – PS*
 - Mod to what?
 - What feedback?

## Examples of commits that could be better:
*“Tweaks to sensor view to support showing Holes and layout in render WindowTitleText” - DE*
 - This is a good summary of the changes; however, using WindowTitleText assumes (probably too much) specific knowledge and it is ambiguous.
 - Tweaks should either not be used (see below for better message) or should be clarified in the description.
   - “Adds support to sensor view for showing…”

*“Updates to the Sensor window in limited developer*

*Added a zoom function, with buttons and selector and map screen” - DE*
 - Summary could be better but is ok 
 - Description says exactly what the commit changes which is good
 - The commit is not atomic; zoom and map selector should be in separate commits.

*“Updated README for VltEncoder example project.” - RA*
 - Good atomic commit with good summary
 - Could also include have a reason why in the description i.e. for new XYZ functionality, for changes since blah, blah.

*“Added benchmark tests for different fillers on the move. Updated BenchmarkDotNet to version 0.10.9.0” – BQ*
 - This should be two commits
 - Each summary is adequate: it describes what tests were added.

*“Fix issues with training on device

*Tests were not being dispensed as droplets didn't return to circular shape.*  
*Changes to initialisation parameters*  
*Deal with failed tests better (duration was 0 so scored very highly)*  
*Handle if test never started” - PF*
 - Good summary with more detail of the commit with changes and reasons why
 - Should be separate commits – not atomic

## Examples of good commits:
*“Fix MasterBuilder bin/obj paths in teardown script.” - TB*
 - Good summary saying what it’s fixing and where (why is implied)
 - Atomic

*“Disable blocking regions in GUI by default” – EH*
 - Good summary and atomic

*“Adding Overlay for membrane sequencing electrodes” – PS*

*“Switch back to log4net 2.0.8, since reverting didn't fix Jenkins build.” – RA*
 - Says what it does and why and atomic

*“Adds interfaces to Comms.Commands to reduce coupling to specific Comms implementation” – RA*
 - What and why and atomic

*“Fix issue HardwareSupervisor Dispose for heater temperature*

*https://www.wrike.com/open.htm?id=174791299  
http://morpheus/redmine/issues/860#change-1306  
Issue was during turning off all heaters. Exception occurs when HardwareSupervisor is disposed.*

    Collection was modified; enumeration operation may not execute.  

*This was due to a race condition between checking whether all heaters are turned off and turning the next heater off. To stop them running at the same time change from using a parallel foreach to normal foreach.” - PF*
 - Atomic
 - Link to issue
 - The bug, the reason, the change and why it fixes the bug


## Simple things may not need a lot of detail:
*“Code formatting tidy up”*  
*“Removing old files”*  
*“Tidying up a few comments”*  

