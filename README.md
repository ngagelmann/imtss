# iMTSS

Integrated two-axis prognostic framework for allogeneic haematopoietic cell transplantation in myelofibrosis.

Live calculator: **https://ngagelmann.github.io/imtss/**

## What this is

Outcome after allogeneic transplantation for myelofibrosis is driven by two largely
independent axes:

- a **disease axis**, built from molecular and haematologic features, which predicts **relapse**
- a **host and structural axis**, built from patient and donor features, which predicts **non-relapse mortality**

The two are nearly independent, sharing 3.4% of their variance. Recombined they estimate
overall survival; separated they indicate *which* of the two failure modes threatens a given
patient, and therefore which class of intervention is relevant.

The calculator returns, for an individual patient:

- predicted overall survival at 5 years
- predicted relapse and non-relapse mortality at 2 years
- the patient's position on the two-axis map

## Model

| Endpoint | Method | Horizon |
|---|---|---|
| Overall survival | Cox proportional hazards | 5 years |
| Relapse | Fine and Gray subdistribution hazard | 2 years |
| Non-relapse mortality | Fine and Gray subdistribution hazard | 2 years |

Developed in 1,550 patients undergoing first allogeneic transplantation, split 60/40 into a
development set (n = 930) and a held-out validation set (n = 620). Standardisation constants,
score centring and baseline hazards are taken from the development set only.

Validation concordance: 0.62 for overall survival, 0.69 for relapse, 0.63 for non-relapse
mortality. Evaluated on the full cohort with out-of-fold scoring, overall survival
discrimination was 0.640 (95% CI 0.616 to 0.662), higher than every established
disease-specific and transplant-specific comparator tested in its own validated population.

## Interpretation

The **continuous estimate is the instrument**. Risk bands are a communication layer: they
reduce discrimination relative to the continuous score, and two patients on opposite sides of
a boundary differ far less than their labels suggest.

The **two-axis map is mechanistic, not prognostic**. It indicates which axis dominates a
patient's risk, not how large that risk is. The region labelled *No dominant axis* therefore
spans patients who are genuinely low risk on both axes and patients who are merely below the
high-risk threshold of each; the magnitude of risk is given by the survival estimate.

Estimates falling outside the range observed in the development cohort are flagged as
extrapolations and should be read as a direction of risk rather than as a probability.

## Deploying

1. Create a repository named `imtss`.
2. Upload the contents of this folder to the repository root.
3. Settings, then Pages, then set Source to `Deploy from a branch`, branch `main`, folder `/ (root)`.
4. The site appears at `https://ngagelmann.github.io/imtss/` within a few minutes.

`index.html` is fully self-contained: no build step, no dependencies, no external requests.
Everything runs in the browser, so no entered patient data leaves the device.

## Files

| File | Purpose |
|---|---|
| `index.html` | The calculator, self-contained |
| `calc_config.json` | Frozen model coefficients, standardisation constants, baselines and band thresholds |
| `CITATION.cff` | Citation metadata |
| `LICENSE` | MIT |
| `.nojekyll` | Serves the files as-is |

## Limitations

Prognostic, not causal. The donor and host associations are observational and confounded by
indication, so the map identifies candidate levers and informs the conversation; it does not
establish that changing a factor changes the outcome. The framework is at present internally
validated only, in a held-out set drawn from the same multicentre cohort.

Not a medical device. Informational only; does not replace clinical judgement.

## Citation

See `CITATION.cff`.
