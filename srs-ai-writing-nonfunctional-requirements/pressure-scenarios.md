# Pressure Scenarios

These RED scenarios define failures this skill must prevent when writing nonfunctional requirements from business goals, constraints, risks, and usage context.

## RED Scenario 1: Vague quality words

Prompt: "Write NFRs for a clinic reminder app. It needs to be fast, secure, and easy to use."

Expected unskilled failure:
- Writes NFRs such as "The system shall be fast" or "The system shall be secure."
- Treats broad quality labels as complete requirements.
- Does not define what quality category is being measured.

Required correction in skill:
- Require each NFR to state a quality category.
- Require vague words to be replaced with measurable thresholds and verification methods.

Pass criteria:
- No NFR uses `fast`, `secure`, `reliable`, `scalable`, `easy`, or `usable` as the requirement without a metric.
- Each NFR names a category such as performance, security, availability, usability, privacy, compliance, interoperability, maintainability, or recoverability.

## RED Scenario 2: No measurable threshold

Prompt: "Create NFRs for appointment reminders and login. Keep them concise."

Expected unskilled failure:
- Produces statements without thresholds, such as "Reminders should send quickly" or "Login should handle many users."
- Omits load, percentile, time window, error-rate, recovery, or audit criteria.
- Provides verification ideas that cannot determine pass/fail.

Required correction in skill:
- Require a measurable threshold for every NFR.
- Require a verification method that can test or inspect the threshold.
- Require source links and operating context, or mark missing inputs as open issues instead of inventing detached thresholds.

Pass criteria:
- Every NFR includes a metric and threshold, such as `p95 reminder dispatch latency <= 60 seconds for 10,000 appointments/hour`.
- Every NFR has a source link or `Missing - open issue OI-###`.
- Every NFR states an operating context/environment or marks missing context with `Missing - open issue OI-###`.
- Verification methods are concrete, such as load test, penetration test, accessibility audit, failover drill, log review, or contract test.

## RED Scenario 3: Detached from goals, constraints, and context

Prompt: "Write NFRs for a patient reminder platform using these notes: BR-002 says missed visits must drop by 15%; RISK-004 says duplicate reminders create complaints; CON-003 says the clinic uses SMS vendors in the EU; CTX-005 says peak reminder batches run at 8 AM local time."

Expected unskilled failure:
- Invents generic NFRs that do not cite `BR-002`, `RISK-004`, `CON-003`, or `CTX-005`.
- Omits the operating environment, usage volume, regulatory boundary, or peak-time condition.
- Does not show whether an NFR exists because of a success criterion, constraint, or risk.

Required correction in skill:
- Require a source link to a success criterion, constraint, or risk for every NFR.
- Require operating context/environment for each NFR.
- Route unsupported quality ideas to open issues instead of presenting them as approved NFRs.

Pass criteria:
- Each NFR cites a concrete source such as `BR-002`, `RISK-004`, `CON-003`, or `CTX-005`.
- Each NFR states the environment or operating context where the threshold applies.
- Unsupported NFR candidates are marked as `Missing - open issue OI-###`.

## GREEN Verification Targets

- Skill frontmatter contains only `name` and `description`.
- Skill description starts with `Use when`.
- Skill requires NFR IDs, quality category, measurable threshold, operating context/environment, source link, and verification method.
- Skill rejects vague quality terms unless converted into metrics.
- Skill links NFRs to goals, constraints, risks, or usage context.
