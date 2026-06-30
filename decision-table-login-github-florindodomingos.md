# Decision Table Testing — GitHub Login

**Test Technique:** Decision Table Testing (ISTQB Foundation Level)
**Feature under test:** GitHub Login page (https://github.com/login)
**Author:** [Florindo Domingos]
**Date:** June 2026

---

## 1. Objective

Apply the **Decision Table Testing** technique to the GitHub login functionality, in order to identify every possible combination of input conditions and derive the corresponding test cases, ensuring full coverage of the business rules.

## 2. Conditions Under Analysis

For this exercise, only two input conditions were considered:

| Condition | Description |
|---|---|
| **C1** | Is the e-mail (or username) correct? |
| **C2** | Is the password correct? |

With 2 binary conditions (Yes/No), we obtain **2² = 4 possible combinations**, resulting in a Decision Table with 4 rules.

## 3. Decision Table

| | **Rule 1** | **Rule 2** | **Rule 3** | **Rule 4** |
|---|:---:|:---:|:---:|:---:|
| **C1 — Correct e-mail?** | T | T | F | F |
| **C2 — Correct password?** | T | F | T | F |
| **Action — Outcome** | Successful login | Login rejected | Login rejected | Login rejected |
| **Message displayed** | — (redirects to Dashboard) | "Incorrect username or password." | "Incorrect username or password." | "Incorrect username or password." |

> **Security note:** GitHub, like most modern platforms, always displays the **same generic error message** regardless of whether the e-mail or the password is incorrect. This is a deliberate security measure to prevent *user enumeration* — i.e., to stop an attacker from discovering which e-mails are registered in the system based on the error message shown. As a result, Rules 2, 3 and 4 share the same action and message — something a QA analyst should identify and validate as expected behavior, not unnecessary duplication.

## 4. Test Cases

| Field | TC01 | TC02 | TC03 | TC04 |
|---|---|---|---|---|
| **ID** | TC_LOGIN_01 | TC_LOGIN_02 | TC_LOGIN_03 | TC_LOGIN_04 |
| **Title** | Login with correct e-mail and correct password | Login with correct e-mail and incorrect password | Login with incorrect e-mail and correct password | Login with incorrect e-mail and incorrect password |
| **Associated rule** | R1 | R2 | R3 | R4 |
| **Precondition** | User has a valid GitHub account | User has a valid GitHub account | — | — |
| **Test data** | E-mail: valid.user@email.com<br>Password: ValidPassword123! | E-mail: valid.user@email.com<br>Password: WrongPassword999! | E-mail: doesnotexist@email.com<br>Password: ValidPassword123! | E-mail: doesnotexist@email.com<br>Password: WrongPassword999! |
| **Steps** | 1. Go to github.com/login<br>2. Enter the correct e-mail<br>3. Enter the correct password<br>4. Click "Sign in" | 1. Go to github.com/login<br>2. Enter the correct e-mail<br>3. Enter an incorrect password<br>4. Click "Sign in" | 1. Go to github.com/login<br>2. Enter a non-existent e-mail<br>3. Enter a password<br>4. Click "Sign in" | 1. Go to github.com/login<br>2. Enter a non-existent e-mail<br>3. Enter an incorrect password<br>4. Click "Sign in" |
| **Expected result** | Login is successful; the user is redirected to the Dashboard | Login is rejected; "Incorrect username or password." is displayed; user remains on the login page | Login is rejected; "Incorrect username or password." is displayed; user remains on the login page | Login is rejected; "Incorrect username or password." is displayed; user remains on the login page |
| **Priority** | High | High | Medium | Medium |
| **Type** | Positive path (Happy Path) | Negative path | Negative path | Negative path |

## 5. Conclusion

Applying the Decision Table made it possible to systematically identify the 4 possible combinations between the two conditions analyzed, ensuring that no login scenario was overlooked. This exercise demonstrates how the **Decision Table Testing** technique (black-box, specification-based — ISTQB CTFL) helps derive test cases in a structured, traceable way, reducing the likelihood of redundant or missing tests.

As an additional QA observation, this case reinforces the importance of not assuming that "more conditions = more distinct outcomes": for security reasons, 3 of the 4 rules produce the same observable result, which is itself a behavior worth validating.

---
*Exercise completed as part of QA Analyst training (ISTQB Foundation Level).*
