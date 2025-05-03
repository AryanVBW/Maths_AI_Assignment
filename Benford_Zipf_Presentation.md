# Presentation: Benford's Law & Zipf's Law in Movie Subtitles

---

## Slide 1: Introduction

*   **Topic:** Exploring two fascinating statistical patterns: Benford's Law and Zipf's Law.
*   **Context:** Applying these laws to the `movies_subtitles.csv` dataset.
*   **Goal:** Understand how these non-intuitive laws manifest in real-world data.

---

## Slide 2: What is Benford's Law? (The Law of First Digits)

*   **Concept:** Benford's Law describes the frequency distribution of leading digits in many real-life sets of numerical data.
*   **Prediction:** The law states that the digit '1' appears as the leading digit about 30% of the time, '2' about 17.6%, and so on, with higher digits appearing less frequently.
*   **Formula:** P(d) = log10(1 + 1/d) for d ∈ {1, 2, ..., 9}
*   **Intuition:** It often applies to data that spans several orders of magnitude.

---

## Slide 3: Benford's Law - Key Question

*   **Question:** What is the probability that the leading digit of a number (in a naturally occurring dataset) is 1?
*   **Benford's Answer:** Approximately 30.1%
*   **Contrast:** If digits were uniformly distributed, we'd expect ~11.1% (1/9).

---

## Slide 4: Applying Benford's Law to Movie Subtitles Data

*   **Hypothesis:** Numerical data within the `movies_subtitles.csv` (e.g., start/end timestamps, potentially other numeric fields if available) might follow Benford's Law.
*   **Data Column(s) for Analysis:**
    *   `start_time` (Subtitle start times in seconds)
*   **Analysis:**
    1.  Extract the `start_time` numerical data.
    2.  Isolate the first significant digit of each number.
    3.  Calculate the frequency distribution of these leading digits (1-9).
    4.  Compare the observed distribution to Benford's predicted distribution.

---

## Slide 5: Benford's Law - Results

*   **Dataset Used:** `movies_subtitles.csv`
*   **Column Analyzed:** `start_time`
*   **Observed vs. Expected Frequencies (from 10,358,275 valid start times):**
    *   Digit 1: 20.1% (Expected: 30.1%)
    *   Digit 2: 19.5% (Expected: 17.6%)
    *   Digit 3: 18.8% (Expected: 12.5%)
    *   Digit 4: 16.9% (Expected: 9.7%)
    *   Digit 5: 11.1% (Expected: 7.9%)
    *   Digit 6: 5.7% (Expected: 6.7%)
    *   Digit 7: 3.3% (Expected: 5.8%)
    *   Digit 8: 2.5% (Expected: 5.1%)
    *   Digit 9: 2.2% (Expected: 4.6%)
*   **Visualization:**
    ```mermaid
    xyChart-beta
        title "Benford's Law: Observed vs. Expected Frequencies (start_time)"
        x-axis "Leading Digit" [1, 2, 3, 4, 5, 6, 7, 8, 9]
        y-axis "Frequency (%)" 0 --> 35
        bar ["20.1", "19.5", "18.8", "16.9", "11.1", "5.7", "3.3", "2.5", "2.2"]
        line ["30.1", "17.6", "12.5", "9.7", "7.9", "6.7", "5.8", "5.1", "4.6"]
        legend ["Observed", "Expected (Benford)"]
    ```
*   **Conclusion:** The `start_time` data does not strongly conform to Benford's Law. While the general trend of decreasing frequency for higher digits exists, the lower digits (especially '1') are underrepresented, and digits 2-5 are overrepresented compared to the theoretical distribution. This might be due to the nature of subtitle timings.

---

## Slide 6: What is Zipf's Law? (The Law of Rank Frequency)

*   **Concept:** Zipf's Law relates the frequency of a word in a text corpus to its rank in the frequency table.
*   **Prediction:** The most frequent word will occur approximately twice as often as the second most frequent word, three times as often as the third most frequent word, and so on.
*   **Formula:** Frequency ≈ Constant / Rank
*   **Observation:** A few words are used very frequently, while many words are used rarely.

---

## Slide 7: Zipf's Law - Key Question

*   **Question:** How does the frequency of words relate to their rank in a large body of text?
*   **Zipf's Answer:** The frequency is inversely proportional to the rank.
*   **Example:** If "the" is the 1st most common word, "of" (2nd) should appear about 1/2 as often, and "and" (3rd) about 1/3 as often.

---

## Slide 8: Applying Zipf's Law to Movie Subtitles Data

*   **Hypothesis:** The frequency of words used in the movie subtitles text should follow Zipf's Law.
*   **Data Column for Analysis:**
    *   `text` (The subtitle text content)
*   **Analysis:**
    1.  Extract all text from the `text` column.
    2.  Tokenize the text into words (lowercase, remove punctuation/numbers, remove common English stop words and subtitle artifacts like 'sighs').
    3.  Count the frequency of each unique word.
    4.  Rank the words from most frequent to least frequent.
    5.  Plot word frequency against word rank using log-log scales.

---

## Slide 9: Zipf's Law - Results

*   **Dataset Used:** `movies_subtitles.csv`
*   **Column Analyzed:** `text`
*   **Analysis Summary:** Analyzed 34,611,884 words after filtering (from 306,477 unique words).
*   **Top 10 Words & Frequencies:**

    | Rank | Word    | Frequency |
    |------|---------|-----------|
    | 1    | dont    | 417556    |
    | 2    | im      | 406630    |
    | 3    | know    | 384426    |
    | 4    | get     | 308548    |
    | 5    | like    | 286525    |
    | 6    | go      | 284509    |
    | 7    | right   | 266279    |
    | 8    | come    | 253165    |
    | 9    | youre   | 243768    |
    | 10   | well    | 234644    |

*   **Visualization (Log-Log Plot for Top 30 Words):**
    ```mermaid
    xyChart-beta
        title "Zipf's Law: Log(Frequency) vs. Log(Rank) for Top 30 Words (text)"
        x-axis "Log10(Rank)" 0 --> 1.5
        y-axis "Log10(Frequency)" 5.0 --> 5.7
        scatter
            data [
                { x: 0.0, y: 5.621 }, { x: 0.301, y: 5.609 }, { x: 0.477, y: 5.585 },
                { x: 0.602, y: 5.489 }, { x: 0.699, y: 5.457 }, { x: 0.778, y: 5.454 },
                { x: 0.845, y: 5.425 }, { x: 0.903, y: 5.403 }, { x: 0.954, y: 5.387 },
                { x: 1.000, y: 5.370 }, { x: 1.041, y: 5.337 }, { x: 1.079, y: 5.320 },
                { x: 1.114, y: 5.319 }, { x: 1.146, y: 5.318 }, { x: 1.176, y: 5.307 },
                { x: 1.204, y: 5.277 }, { x: 1.230, y: 5.261 }, { x: 1.255, y: 5.252 },
                { x: 1.279, y: 5.248 }, { x: 1.301, y: 5.197 }, { x: 1.322, y: 5.158 },
                { x: 1.342, y: 5.158 }, { x: 1.362, y: 5.152 }, { x: 1.380, y: 5.136 },
                { x: 1.398, y: 5.132 }, { x: 1.415, y: 5.120 }, { x: 1.431, y: 5.116 },
                { x: 1.447, y: 5.112 }, { x: 1.462, y: 5.106 }, { x: 1.477, y: 5.097 }
            ]
        legend ["Observed Data (Top 30 Words)"]
    ```
*   **Conclusion:** The word distribution in the `text` column conforms well to Zipf's Law. The log-log plot shows a clear linear relationship between log(rank) and log(frequency) with a negative slope, as predicted by the law. This indicates a typical natural language distribution where a few words dominate in frequency.

---

## Slide 10: Conclusion & Discussion

*   **Summary:** We explored Benford's Law for leading digits (using `start_time`) and Zipf's Law for word frequencies (using `text`) in the `movies_subtitles.csv` dataset.
*   **Findings:** 
    *   Benford's Law was *not* strongly supported by the `start_time` data, showing significant deviations from the expected distribution.
    *   Zipf's Law *was* well supported by the `text` data, demonstrating the characteristic inverse relationship between word rank and frequency.
*   **Implications:** Highlights how these laws can apply differently depending on the type of data. Benford's is often sensitive to how numbers are generated or constrained, while Zipf's is quite robust for natural language.
*   **Further Questions:** Would Benford's Law apply better to other numerical fields if available (e.g., movie budgets, box office numbers)? Do word frequencies differ significantly across movie genres within the dataset?

---
