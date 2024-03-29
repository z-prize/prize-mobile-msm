# Accelerating MSM on Mobile



Prize Sponsor: [Ocelot](https://ocelotlabs.xyz/)

Prize Architect: [cLabs](https://clabs.co/)

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

-   All submissions will be tested on the [Samsung Galaxy A13 5G](https://www.devicespecifications.com/en/model/46da57d2) (Model SM-A136ULGDXAA with [SoC MediaTek Dimensity 700 (MT6833)](https://www.mediatek.com/products/smartphones-2/dimensity-700)).
-   The baseline will be the Arkworks MSM implementation over BLS12-377 G1. Submissions must beat this baseline by at least 10% in order to be eligible for the prize.
-   The baseline Android application including a [test harness] is provided, and may be used by competitors as the basis for their submission. Competitors may create their own application and test harness.

[test harness]: https://github.com/celo-org/zprize-mobile-harness

Competitors will be provided with the target device either by having it purchased for them and sent to their address, or by being reimbursed for their purchase. Teams with at least two members may request two devices.

The test harness, which includes benchmarking code and will be used as the baseline implementation
for judging, is available at
[github.com/celo-org/zprize-mobile-harness](https://github.com/celo-org/zprize-mobile-harness).

### Constraints

-   Submission must run on Android 12 (API level 32).
-   MSM must be over BLS12-377 G1 with scalars from the associated field.
-   Submissions may take advantage of any hardware features of the target device (Samsung Galaxy A13 5G).
    - E.g. The SoC in the A13 5G can run 32-bit and 64-bit instruction sets. Submissions may use any
        supported instruction set for their implementation.
    - E.g. This device also has 8 cores in a 2.6 BIG.little architecture. Optimizations may
        take advantage of this layout to optimize their computations.
-   Submissions may be written in any programming language.
-   If competitors create their own test harness, it must be determined by the judges to be running a benchmark equivalent to the provided test harness.
    - Note that the input to the MSM routine are arkworks representations of `bls377::G1Affine` and `<bls377::Fr as PrimeField>::BigInt` at version `0.3.0`.
      If you would like to use a different representation, you should contact the judging team to determine if it is permissible.
-   Submissions must not cause stability issues when run on the target device.
-   Submissions must not require the device to be rooted (i.e. it must be possible to integrate the solution into an app on the Google Play Store, although competitors do not need to do so for the competition).
-   Submissions must include documentation, in English, to understand the optimization approach.
-   Submissions must include tests using, at a minimum, the provided test vectors.
-   The judges must be able to build and run the submitted application. Any documentation on building the application should be included in the submission.

## Timeline

June 10 - Competition begins

August 4 - Mid-competition submission due

October 1 - Final submission due

### Mid-competition Submission

The mid-competition submission gives an opportunity for competitors to confirm they're submission
meets all the requirements and get a score according to the official judging procedure. Competitors
are not required to submit their work for the mid-competition submission.

By August 4th (23:59 GMT), competitors may submit a working version of their final submission. If
they do, the judging team will evaluate it to ensure it fulfills all the constraints. If so, they will
run the submission using the same benchmarking procedure that will be used for judging the final
submissions, as outlined below, and report the result. If there are any issues, the judging team will
work to resolve them with the competitor.

Submissions do not need to be open-sourced for the mid-competition submission, but the source code
does need to be shared with the judging team, who will compile the application from source following
the same procedure as will be used for the final submission.

For the submission, please send an email to the judging team with the source code, build instructions,
and documentation of optimization techniques used. Sharing a git repository endpoint, or an
archive (e.g. `.tar.gz` or `.zip`) are two acceptable options for sharing source code and documentation.
Please include your team name with the submission. Once your submission has been evaluated, the judging
team will respond with any concerns related to constraints, and with detailed performance numbers.

After the submissions are evaluated, the sponsors and judging team may share preliminary rankings, and
rough overall performance numbers in a blog post. If you would like to opt out of having your team information
included please let us know in the email when you send in your mid-competition submission.

### Final Submission

The final submission of the application is due by October 1st (23:59 GMT).

The final submission must meet all the constraints listed above, including that the application be
buildable from source and installable as an app on the target device. If any constraints are not met,
the submission will not be judged, and will not be eligible to win any prizes. As a result, it is
**highly recommended** that teams send a version of the submission to the judging team at least 3
days in advance of the deadline so there is time to inform the team of any constraints that are not
met (e.g. that the application does not build with the given instructions). After the deadline,
absolutely no modification can be made that could reasonably affect the benchmarked performance. Any
alterations to auxiliary constraints (e.g. licensing) will only be allowed if it does not affect the
fairness of the competition, at the discretion of the judging team.

For the submission, please send an email to the judging team with the source code, build instructions,
and documentation of optimization techniques used. Sharing a git repository endpoint, or an
archive (e.g. `.tar.gz` or `.zip`) are two acceptable options for sharing source code and documentation.
Please include your team name with the submission. Once your submission has been evaluated, the judging
team will respond with any concerns related to constraints, and with detailed performance numbers.

The judging team will evaluate all received submissions that meet the constraints. The judging team
will communicate with the individual teams to inform them of their submission's evaluated
performance and give an opportunity to raise any concerns (e.g. if the evaluated performance is far
out of line with the teams own benchmarking). Once all submissions have been evaluated, and any
concerns about the evaluated performance numbers are resolved, the sponsorship team will announce
the results!

#### Judging team

Victor Graf:
 * Email: victor.graf@clabs.co
 * GitHub: nategraf

Michael Straka:
 * Email: michael.straka@clabs.co
 * GitHub: mstraka100

## Judging

Submissions will be analyzed for correctness, performance, and stability.

All submissions are required to be open-sourced. The judging team will review the source code, and will build the executable to be judged from this source code according to the instructions provided in the submission documentation. Note that if your solution requires particular build flags or a particular compiler version, it should be referenced in the build documentation.

### Functionality

To be suitable for the judging process, each app should copy as closely as possible the behavior of the provided test harness. In particular, its input and output behavior should be identical. The app should be able to take in two files as input: one file containing a list of n scalar vectors, one per line, and another file containing a list of n curve point vectors, one per line, where the i-th scalar vector is the same length as the i-th curve point vector. The app should sequentially perform n separate MSM instances, one per vector, and output two files. One file should contain the n output curve elements, one line per MSM instance. The other should contain the n wall-clock times, in milliseconds, taken to execute the MSM instances, one per line, in addition to one more line containing the mean time across all n previous times. All point and point vectors should encoding equivalently to the arkworks point serialization format at version `0.3.0`. Either the compressed or uncompressed formats may be used, although the uncompressed format is recommended. If there are any questions, please refer to the reference implementation or contact the judging team listed above.

### Correctness

A collection of static test vectors will be provided as a file, and the submitted application should include functionality to load and run the test vectors as a basic correctness test. Test vectors will include instances of various sizes and some important edge cases. The provided test harness includes this functionality and may be used as a reference. The judges will validate that these test vectors are correctly included and will validate the results.

Additionally, the prize committee will sample at least 10 randomly chosen MSM instances and supply them to the application through a new test vector file. MSM instances in the test vectors will be of various sizes. The results will be compared to the result as computed in a separate MSM implementation, such as the arkworks library.

### Performance

To evaluate the performance of each submission, the submission application should perform a number of MSM trials, with the final score determined as the Mean Latency across all trials.

Each trial must sample 2^16 elements and scalars at random from BLS12-377 G1 and the scalar field, then compute the multi-scalar multiplication. Latency of the MSM will be measured as the wall-clock time from when the input is provided to the MSM routine (i.e. after the elements have been sampled) to when the result is returned.

A number of trials will be conducted until a stable Mean Latency is confidently estimated for the submission. At a minimum, this will be 1000 trials. Additional trials may be conducted if a stable mean is not observed.

The provided test harness template includes an implementation for the benchmarking procedure described above, and should be used by competitors as a reference.

All trials for the final judging will be conducted on a single target device, at full charge, in airplane mode, and placed in a temperature controlled environment. All reasonable efforts will be made to ensure a consistent judging environment for all submissions.

## Prize Allocation

Prizes will be distributed from the total Prize Reward according to a Rank-Weighted Performance-based scoring system.
The baseline score of each competitor's solution will be measured in Mean Latency as described above, and will be used to determine the rank of the competitors, with the lowest Mean Latency resulting in the 1st rank.
In order to calculate the prize share, the multiplicative inverse of the Mean Latency will be used as a weighting score for each qualifying submission (i.e. submissions that pass all constraints, including beating the baseline by at least 10%).
Additionally, a Rank-Based multiplier will be applied to each competitor's Inverse Latency to determine their final score and resulting Prize Payout.
The final Prize Payout will be determined as the submission Inverse Latency, divided by the sum of the Inverse Latencies for all qualifying submissions, and multiplied by the Rank Multipliers.

**Baseline Latency: 3000 ms**

**Total Prize: $375,000**

|  | RANK | Latency | Rank Multiplier | Weighted Score | Prize Share | Prize Payout |
|--|--|--|--|--|--|--|
| Alice | 1st | 1400 | 8x | 8/1400 | .622 | $233,249 |
| Bob | 2nd | 2200 | 5x | 5/2200 | .247 | $92,769 |
| Carrol | 3rd | 2500 | 3x | 3/2500 | .131 | $48,982 |
| Dave | 4th | 2650 | 0x | 0/2650 | 0 | $0 |
| Eve | 5th | 2900 | 0x | 0 (did not qualify) | 0 | $0 |
| SUM |  |  |  |  |  | $375,000 |

- Weighted Score =  Inverse Latency *  Rank Multiplier
- Prize Share  =  Weighted Score / SUM of  all Weighted Scores
- Prize Payout  =  Prize Share  * Total Prize Reward

Baseline Latency mentioned above is an example, and not the value that will be used.
Please note that prize sponsors reserve the right to in good faith reduce or increase a competitors score if doing so falls within the spirit of discouraging “loophole” solutions that are useless to the goals of the prize and in encouraging solutions that are particularly novel or creative.

Finalized Rank Multipliers will be as follows:
* 8x for 1st place
* 5x for 2nd place
* 3x for 3rd place
* 0x for 4th place and below

Following the end of the competition, the sponsorship team will reach out to winning teams to
arrange for them to receive their prize.

## Notes

All submission code must be open-sourced at the deadline for final submission (October 1st). Code and documentation must be dual-licensed under both the MIT and Apache-2.0 licenses.

## Questions

If there are any questions about this prize, please contact victor@clabs.co

### Hardware & Benchmarks Rationale

We’ve chosen the Samsung Galaxy A13 5G as a representative Android device, with specifications similar to older higher-end devices and new budget devices, and as a result represents the kind of hardware that is common today in wealthy markets, and will become common over the next 3-5 years in middle income markets. It is also widely available and relatively inexpensive.

We’ve chosen to target Android specifically, and not to include iOS, to keep the competition focused and because Android is by far the more common platform for users globally.
