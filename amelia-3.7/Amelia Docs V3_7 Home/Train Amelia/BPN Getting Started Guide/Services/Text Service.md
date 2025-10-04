{% version "3.x" %}
The text service provides manipulation, search, and matching operations for BPN Script tasks and libraries.
# Methods
## searchExact
    Table<String, String, Double> searchExact(@NonNull Set<String> values, @NonNull String sentence, @NonNull boolean caseSensitive)
Searches for a set of values in a sentence. Returns a map of scores, keyed by pairs (value, matching token).

| Parameter | Description |
| ----|----|
| values | Set of values to match the sentence tokens against |
| sentence | Sentence with one or more single word tokens |

## bestExactMatch
    Triple<String, String, Double> bestExactMatch(@NonNull Set<String> values, @NonNull String sentence, @NonNull boolean caseSensitive)
Finds the closest matching occurrence in the specified search. Returns a map of scores, keyed by pairs (value, matching token).

| Parameter | Description |
| ----|----|
| values | Set of values to match the sentence tokens against |
| sentence | Sentence with one or more single word tokens |

## searchFuzzy
    Table<String, String, Double> searchFuzzy(@NonNull Set<String> values, @NonNull String sentence, @NonNull Double tokenMatchThreshold)
Fuzzily matches a set of strings against a sentence. Returns a result table.

| Parameter | Description |
| ----|----|
| values | Set of values to match the sentence tokens against |
| sentence | Sentence with one or more single word tokens |
| tokenMatchThreshold | Token similarity (0..1) threshold for a match |

## bestFuzzyMatch
    Triple<String, String, Double> bestFuzzyMatch(@NonNull Set<String> values, @NonNull String sentence, @NonNull Double tokenMatchThreshold)
Finds the closes fuzzy match in the specified search. Returns a result table.

| Parameter | Description |
| ----|----|
| values | Set of values to match the sentence tokens against |
| sentence | Sentence with one or more single word tokens |
| tokenMatchThreshold | Token similarity (0..1) threshold for a match |

## searchSemantic
    Table<String, String, Double> searchSemantic(@NonNull Set<String> values, @NonNull String sentence, @NonNull Double tokenMatchThreshold)
Semantically matches a set of strings against a sentence. Returns a result table.

| Parameter | Description |
| ----|----|
| values | Set of values to match the sentence tokens against |
| sentence | Sentence with one or more single word tokens |
| tokenMatchThreshold | Token similarity (0..1) threshold for a match |

{% /version %}
