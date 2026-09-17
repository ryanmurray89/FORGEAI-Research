# Methodology

## Question construction

The benchmark question builder created 66 questions from the clean 423-claim verified corpus.

The set was split into 12 calibration questions and 54 locked evaluation questions.

## Artifact freeze

The calibration, evaluation, combined-question, and manifest artifacts were assigned fixed SHA-256 hashes.

Those hashes formed the identity of the benchmark inputs used by later experiments.

## Calibration isolation

Retrieval-policy calibration loaded only the 12 calibration questions.

The calibration process verified the SHA-256 of the locked evaluation artifact without parsing the evaluation questions.

## Production isolation

Calibration and benchmark preparation were performed against isolated benchmark artifacts and Chroma collections.

Production Chroma, Brain, and the database were not modified.
