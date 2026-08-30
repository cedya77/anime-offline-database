# Merge decisions

The dataset is built by fusing one entry per provider into a single record. Most of that fusing is
done automatically by a matching probability calculator, which is a heuristic and gets things wrong
in both directions: it welds separate seasons together, and it leaves the same anime sitting in two
records because two providers spell the title differently.

The two files here are the record of the cases that were decided by hand instead. They are inputs to
the build, not outputs of it, which is why they are versioned separately from the dataset.

## merge.lock

A list of groups. Every URI in a group refers to the same anime, and the grouping is final: entries
covered by a lock skip the probability calculator entirely, so a provider editing a title or an
episode count cannot silently regroup them later.

The build maintains this file on its own in two cases. When a provider deletes an entry its URI is
dropped from the group, and when a provider renumbers an entry the URI is rewritten in place. Nothing
else changes a lock once it is written.

## checked-isolated-entries.txt

Entries that appear on exactly one provider and were confirmed to genuinely belong to only one, as
opposed to being a merge the calculator missed. Without this the two cases are indistinguishable, and
a correctly isolated entry looks forever like unfinished work.

## Contributing

Both files are safe to propose changes to. A grouping that is wrong, or a merge that should have
happened and did not, is worth an issue or a pull request either way.
