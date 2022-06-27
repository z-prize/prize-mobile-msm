# Accelerating MSM on Mobile



Prize Sponsor: Celo

Prize Architect: Celo

## Prize Description

### Summary

Proving on mobile devices is a transformative technology for applications including private transactions, self-sovereign identity, and scalable computation. Multi-scalar multiplication (MSM) is a core operation for producing zkSNARKs, and it is the primary bottleneck and barrier for deployment of proving on mobile. This prize will focus on minimizing latency of computing MSM in native mobile applications.

### Optimization Objective (1-sentence)

Achieve the lowest latency in computing a multi-scalar multiplication on a mobile device.

#### Detail

This prize focuses on [variable-base MSM](https://cryptojedi.org/peter/data/eccss-20130911b.pdf), which is widely used in zkSNARKs. Formally, variable-base MSM takes as an input vector of elliptic curve points

$$[P_1, P_2,..., P_n]$$

and an input vector of elements from the associated prime-order scalar field

$$[k_1, k_2, ..., k_n]$$

Here, n is the input vector length (i.e., the number of elements in a vector).

The output is an elliptic curve point, Q

$$Q=\sum^n_{i=1} k_i*P_i$$

### Hardware & Benchmarks

-   All submissions will be tested on the [Samsung Galaxy A13 5G](https://www.devicespecifications.com/en/model/46da57d2) ([SoC MediaTek Dimensity 700 (MT6833)](https://www.mediatek.com/products/smartphones-2/dimensity-700)).
-   The baseline will be the Arkworks MSM implementation over BLS12-377 G1. Submissions must beat this baseline by at least 10% in order to be eligible for the prize.
-   The baseline Android application including a test harness will be provided, and may be used by competitors as the basis for their submission. Competitors may create their own application and test harness.

Competitors will be provided with the target device either by having it purchased for them and sent to their address, or by being reimbursed for their purchase. Teams with at least two members may request two devices.

### Constraints

-   Submission must run on Android 12 (API level 32).
-   MSM must be over BLS12-377 G1 with scalars from the associated field.
-   Submissions may take advantage of any hardware features of the target device (Samsung Galaxy A13 5G).
-   Submissions may be written in any programming language.
-   If competitors create their own test harness, it must be determined by the judges to be running a benchmark equivalent to the provided test harness.
-   Submissions must not cause stability issues when run on the target device.
-   Submissions must not require the device to be rooted (i.e. it must be possible to integrate the solution into an app on the Google Play Store, although competitors do not need to do so for the competition).
-   Submissions must include documentation, in English, to understand the optimization approach.
-   Submissions must include tests using, at a minimum, the provided test vectors.
-   The judges must be able to build and run the submitted application. Any documentation on building the application should be included in the submission.

## Timeline

June 10 - Competition begins

July 25 - Mid-competition submission due

September 10 - Final submission due

## Judging

Submissions will be analyzed for correctness, performance, and stability.

All submissions are required to be open-sourced. The judging team will review the source code, and will build the executable to be judged from this source code according to the instructions provided in the submission documentation. Note that if your solution requires particular build flags or a particular compiler version, it should be referenced in the build documentation.

### Correctness

A collection of static test vectors will be provided as a file, and the submitted application should include functionality to load and run the test vectors as a basic correctness test. Test vectors will include instances of various sizes and some important edge cases. The provided test harness will include this functionality and may be used as a reference. The judges will validate that these test vectors are correctly included and will validate the results.

Additionally, the prize committee will sample at least 10 randomly chosen MSM instances and supply them to the application through a new test vector file. MSM instances in the test vectors will be of various sizes. The results will be compared to the result as computed in a separate MSM implementation, such as the arkworks library.

### Performance

To evaluate the performance of each submission, the submission application should perform a number of MSM trials, with the final score determined as the Mean Latency across all trials.

Each trial must sample 2^16 elements and scalars at random from BLS12-377 G1 and the scalar field, then compute the multi-scalar multiplication. Latency of the MSM will be measured as the wall-clock time from when the input is provided to the MSM routine (i.e. after the elements have been sampled) to when the result is returned.

A number of trials will be conducted until a stable Mean Latency is confidently estimated for the submission. At a minimum, this will be 1000 trials. Additional trials may be conducted if a stable mean is not observed.

The provided test harness template will include an implementation for the benchmarking procedure described above, and should be used by competitors as a reference.

All trials for the final judging will be conducted on a single target device, at full charge, plugged in, and placed in airplane mode. All reasonable efforts will be made to ensure a consistent judging environment for all submissions.

## Prize Allocation

Prizes will be distributed from the total Prize Reward according to a Rank-Weighted Performance-based scoring system. The baseline score of each competitor's solution will be measured in Mean Latency as described above, and will be used to determine the rank of the competitors, with the lowest Mean Latency resulting in the 1st rank. In order to calculate the prize share, the multicative inverse of the Mean Latency will be used as a weighting score for each qualifying submission (i.e. submissions that pass all constraints, including beating the baseline by at least 10%). Additionally, a Rank-Based multiplier will be applied to each competitor's Inverse Latency to determine their final score and resulting Prize Payout. The final Prize Payout will be determined as the submission Inverse Latency, divided by the sum of the Inverse Latencies for all qualifying submissions, and multiplied by the Rank Multipliers.


**Baseline Latency: 3000 ms**

**Total Prize: $375,000**

|  | RANK | Latency | Rank Multiplier | Weighted Score | Prize Share | Prize Payout |
|--|--|--|--|--|--|--|
| Alice | 1st | 1400 | 4x | 4/1400 | .60 | $225,869 |
| Bob | 2nd | 2200 | 2x | 2/2200 | .19 | $71,867 |
| Carrol | 3rd | 2500 | 1.5x | 1.5/2500 | .13 | $47,432 |
| Dave | 4th | 2650 | 1x | 1/2650 | .08 | $29,832 |
| Eve | 5th | 2900 | 1x | 0 (did not qualify) | 0 | $0 |
| SUM |  |  |  |  |  | $375,000 |

- Weighted Score =  Inverse Latency *  Rank Multiplier[1]
- Prize Share  =  Weighted Score / SUM of  all Weighted Scores
- Prize Payout  =  Prize Share  * Total Prize Reward

Baseline Latency mentioned above is an example, and not the value that will be used. Please note that prize sponsors reserve the right to in good faith reduce or increase a competitors score if doing so falls within the spirit of discouraging “loophole” solutions that are useless to the goals of the prize and in encouraging solutions that are particularly novel or creative. The Rank Multipliers to be used will not be finalized until the number of competitors is finalized, but will be chosen to enable a distribution curve roughly proportional to the example shown given the solutions provided.


## Notes

All submission code must be open-sourced at the time of submission. Code and documentation must be dual-licensed under both the MIT and Apache-2.0 licenses.

## Questions

If there are any questions about this prize, please contact victor@clabs.co


### Hardware & Benchmarks Rationale

We’ve chosen the Samsung Galaxy A13 5G as a representative Android device, with specifications similar to older higher-end devices and new budget devices, and as a result represents the kind of hardware that is common today in wealthy markets, and will become common over the next 3-5 years in middle income markets. It is also widely available and relatively inexpensive.

We’ve chosen to target Android specifically, and not to include iOS, to keep the competition focused and because Android is by far the more common platform for users globally.
