# This is a demo repo for the following issue

I wrote a simple github action to checks if all code owners have approved a PR. This check is triggered by:
pull_request:
types: [review_requested, review_request_removed]
pull_request_review:

And made this a required check on the protected branches.
However when adding a new commit to a pr (which dismisses an approval) the check runs and fails (as it should, since the approval is no longer there). When the codeowner then approves the PR, the check runs again, and it succeeds (as it should).
But the PR is still not able to be merged.
This is because the old failed check (Approval checker / Approval by CODEOWNERS (pull_request)) is still counted.
But the new check (Approval checker / Approval by CODEOWNERS (pull_request_review)) was succeeded.

My question is, why is this counted as 2 separate required checks? Is there a way so it is just checks the latest run if the action and not per trigger type?