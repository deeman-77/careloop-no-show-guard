# CareLoop Clinics — No-Show Guard

## Project Findings

- **Part 1 — Data Engineering:** Cleaned 1,020 original appointment records into 990 valid records after removing 20 duplicates and handling invalid or missing data. Identified 218 no-shows, representing an overall no-show rate of approximately 22.0%.
- **Part 2 — SQL Analytics:** Identified differences in clinic-level attendance patterns. Gomti Nagar Care Point had the highest no-show rate at 33.3%, based on 90 appointments. Longer booking lead times were also associated with higher no-show rates, reaching 60.5% for appointments booked 31 or more days in advance.
- **Part 3 — Machine Learning:** Evaluated Logistic Regression, Decision Tree and Random Forest models. Logistic Regression achieved a test ROC-AUC of 0.789. A classification threshold of 0.35 improved recall to 57.14%, identifying 49 appointments for follow-up in the test set.
- **Part 4 — Generative AI:** Used the Gemini API to analyse 10 follow-up notes and classify them into six predefined root-cause categories. Prompt-guided JSON output and Pydantic validation were used to check the extracted reasons, confidence scores, summaries and recommended actions.

## Business Recommendation

CareLoop Clinics should introduce a risk-based appointment follow-up process to reduce unused appointment slots. The cleaned dataset contained 990 appointments, including 218 no-shows (22.0%), while SQL analysis identified a clinic with a 33.3% no-show rate across 90 appointments and a 60.5% no-show rate among appointments booked 31 or more days in advance. The selected Logistic Regression model achieved a test ROC-AUC of 0.789, and a threshold of 0.35 identified 49 out of 198 test appointments for follow-up, with 57.14% precision and 57.14% recall. The analysis of 10 follow-up notes demonstrates how patient feedback can help identify reasons for missed appointments and guide suitable interventions. Clinics should prioritize higher-risk appointments for reminder calls, investigate clinic-specific attendance patterns and use patient feedback to improve their follow-up process. The risk threshold should be adjusted according to staff capacity and the cost of missed appointment slots.

## Model Selection

**Selected model: Logistic Regression**

Logistic Regression was selected because it achieved the strongest cross-validated ROC-AUC among the evaluated candidate models in the training data (approximately 0.77).

| Evaluation Metric | Result |
|---|---:|
| Test ROC-AUC | 0.789 |
| Classification threshold | 0.35 |
| Test precision | 57.14% |
| Test recall | 57.14% |
| Test appointments flagged | 49 out of 198 |

The 0.35 threshold was selected using out-of-fold training predictions because it achieved a higher F1-score (0.489) than the 0.50 threshold (0.347), while improving recall from approximately 24.9% to 46.7%.

## Limitations

1. **Limited GenAI sample:** Only 10 follow-up notes were analysed. This sample is too small to establish the actual distribution of reasons for missed appointments across all clinics.
2. **Evaluation split:** Only one random train/test split was used. Results may vary with a different split, and the evaluation does not establish how well the model predicts future appointments over time.
3. **Observational data:** The relationships identified between reminders, lead time, patient history and no-shows are associations, not evidence that these factors cause missed appointments.

## Conclusion

CareLoop Clinics — No-Show Guard demonstrates how data engineering, SQL analytics, machine learning and Generative AI can work together to support appointment management. The proposed approach provides a foundation for identifying potentially missed appointments, prioritizing follow-ups and understanding patient-reported reasons for non-attendance.
