# Test Plan — OpenCart QA Suite

**Project:** OpenCart E-Commerce Application  
**Version:** 1.0  
**Author:** Avinabh Singh  
**Date:** March 2026  
**Status:** Active  

---

## Table of Contents

- [Test Plan — OpenCart QA Suite](#test-plan--opencart-qa-suite)
  - [Table of Contents](#table-of-contents)
  - [1. Introduction](#1-introduction)
  - [2. Objectives](#2-objectives)
  - [3. Scope](#3-scope)
    - [In Scope](#in-scope)
    - [Out of Scope](#out-of-scope)
  - [4. Test Strategy](#4-test-strategy)
  - [5. Features to Be Tested](#5-features-to-be-tested)
    - [5.1 Product Search \& Filter](#51-product-search--filter)
    - [5.2 Add to Cart \& Checkout](#52-add-to-cart--checkout)
    - [5.3 Wishlist \& Account Management](#53-wishlist--account-management)
  - [| **Logout** | Session ends, redirected to home, accessing account pages redirects to login. |](#-logout--session-ends-redirected-to-home-accessing-account-pages-redirects-to-login-)
  - [6. Features Not to Be Tested](#6-features-not-to-be-tested)
  - [7. Test Types](#7-test-types)
    - [7.1 Manual Testing](#71-manual-testing)
    - [7.2 UI \& Functional Automation (Cypress)](#72-ui--functional-automation-cypress)
    - [7.3 API Testing](#73-api-testing)
    - [7.4 Performance Testing (JMeter)](#74-performance-testing-jmeter)
  - [8. Tools \& Environment](#8-tools--environment)
    - [Application Under Test](#application-under-test)
    - [Tools](#tools)
    - [Browser Coverage](#browser-coverage)
  - [9. Entry \& Exit Criteria](#9-entry--exit-criteria)
    - [Entry Criteria (before testing begins)](#entry-criteria-before-testing-begins)
    - [Exit Criteria (testing is complete when)](#exit-criteria-testing-is-complete-when)
  - [10. Test Deliverables](#10-test-deliverables)
  - [11. Roles \& Responsibilities](#11-roles--responsibilities)
  - [12. Risks \& Mitigations](#12-risks--mitigations)
  - [13. Schedule](#13-schedule)
  - [14. Assumptions \& Dependencies](#14-assumptions--dependencies)

---

## 1. Introduction

This document outlines the test plan for the **OpenCart e-commerce demo application** available at [https://demo.opencart.com](https://demo.opencart.com). OpenCart is an open-source, PHP-based online shopping cart system widely used in real-world e-commerce projects.

This QA suite is built as a **full-lifecycle testing portfolio project**, covering manual testing, UI/functional automation, API testing, and performance testing. Simulating how a professional QA engineer would approach a real-world application.

---

## 2. Objectives

- Validate the core e-commerce workflows function correctly from a user's perspective.
- Identify functional defects, UI inconsistencies, and edge case failures.
- Demonstrate a complete QA lifecycle: manual → automation → API → performance.
- Build a reusable, maintainable test automation framework using industry-standard tools.
- Produce professional QA artifacts suitable for a real-world project handoff.

---

## 3. Scope

### In Scope

|  # | Module | Description |
|---|---|---|
| 1 | **Product Search & Filter** | Keyword search, sort options, view toggle (grid/list), empty results. |
| 2 | **Add to Cart & Checkout** | Add/update/remove products, cart totals, guest & registered checkout. |
| 3 | **Wishlist & Account Management** | Add/remove wishlist items, account login, profile management. |

### Out of Scope

- Admin panel functionality (beyond API token setup).
- Payment gateway integration (no real transactions on demo).
- Multi-language and multi-currency testing.
- Mobile native app testing.
- Third-party integrations (shipping providers, tax APIs).
- Database testing (requires local installation — may be added in a future phase).

---

## 4. Test Strategy

Testing will be executed in the following layered approach:

```
Manual Testing  →  UI Automation (Cypress)  →  API Testing  →  Performance Testing
```

Each layer builds on the previous:
- **Manual** test cases define what to test.
- **Cypress** automates those same cases for regression speed.
- **API tests** validate the backend independently of the UI.
- **JMeter** stress tests critical endpoints under load.

All automation follows **Page Object Model (POM) + Custom Commands** pattern for maintainability.

---

## 5. Features to Be Tested

### 5.1 Product Search & Filter

| Test Area | Scenarios |
|---|---|
| **Keyword Search** | Valid keyword, partial keyword, case insensitivity, multiple keywords, special characters, numeric-only, very long string, whitespace-only, leading/trailing spaces, SQL injection attempt. |
| **Search Scope** | Search with/without "Search in product descriptions" checked — verify result count differs. |
| **Search Results** | Result count shown, product names/images/prices displayed correctly, clicking product opens correct page. |
| **Sort Options** | Default, Name (A–Z), Name (Z–A), Price (Low > High), Price (High > Low), Rating, Model — verify order changes correctly for each. |
| **Show Per Page** | 10, 25, 50, 75, 100 — verify correct product count and pagination updates. |
| **Pagination** | Next/Previous navigation, direct page number click, URL updates with page param. |
| **View Toggle** | Grid and List view render correctly, toggling maintains current sort and results. |
| **No Results** | Appropriate message shown, no broken layout. |
| **URL & Persistence** | Search params reflected in URL, refreshing URL reloads same results. |
| **Header vs Search Page** | Search from header navigates to results page, search box on results page works independently. |


### 5.2 Add to Cart & Checkout

| Test Area | Scenarios |
|---|---|
| **Add to Cart** | Single product, multiple different products, product with required options (size/colour), product without options, add same product twice (quantity increment), add from search results page, add from category page. |
| **Cart Icon & Count** | Header cart count updates on add, cart dropdown shows correct product name/quantity/price, subtotal in dropdown is accurate. |
| **Cart Page** | All added products listed with correct name/image/price/quantity, unit price and subtotal per item correct. |
| **Quantity Update** | Increase/decrease quantity, set quantity to zero, set invalid value (letters/negative), update reflects in totals. |
| **Remove Item** | Remove single item, remove all items, empty cart message shown when last item removed. |
| **Cart Totals** | Subtotal, eco tax, VAT, and order total calculate correctly after add/update/remove. |
| **Checkout — Options** | Guest checkout option visible, returning customer login option visible, register account option visible. |
| **Checkout — Guest** | All billing fields (first name, last name, email, phone, address, city, postcode, country, region) validated, required field errors on blank submit. |
| **Checkout — Registered** | Billing address pre-filled from account, option to ship to different address available. |
| **Shipping Method** | Available shipping methods listed, selecting a method updates order total. |
| **Payment Method** | Available payment methods listed, selecting a method required to proceed. |
| **Order Confirmation** | Confirm order page shows correct summary, order success page shown after placing, order ID generated. |
| **Negative — Checkout** | Proceed with empty cart, skip shipping/payment selection and submit, invalid email format in guest billing. |


### 5.3 Wishlist & Account Management

| Test Area | Scenarios |
|---|---|
| **Wishlist — Guest** | Clicking wishlist button while logged out shows login prompt, redirects to login page. |
| **Wishlist — Add** | Add product from product page, add from search results, success message shown with link to wishlist, header wishlist count updates. |
| **Wishlist — Duplicate** | Adding an already-wishlisted product removes and re-adds it (toggle behaviour per OpenCart source). |
| **Wishlist — View** | Wishlist page shows correct product name/image/price, product link navigates to correct page. |
| **Wishlist — Add to Cart** | Add to cart directly from wishlist page, item appears in cart. |
| **Wishlist — Remove** | Remove single item, wishlist page reflects removal, empty state shown when all items removed. |
| **Login** | Valid credentials, wrong password, unregistered email, blank email, blank password, all fields blank, "Forgotten Password" link visible. |
| **Forgotten Password** | Valid registered email accepted, invalid email shows error. |
| **Account Dashboard** | Correct name displayed after login, all account menu links visible (Edit Account, Password, Address Book, Wish List, Order History, Transactions, Logout). |
| **Edit Account** | Update first name, last name, email, phone — changes saved and reflected on dashboard. |
| **Change Password** | Valid new password accepted, mismatched confirm password rejected, blank fields rejected. |
| **Address Book** | Add new address, set as default, edit existing address, delete address. |
| **Order History** | Past orders listed with order ID/date/status/total, clicking order shows full order detail. |
| **Logout** | Session ends, redirected to home, accessing account pages redirects to login. |
---

## 6. Features Not to Be Tested

| Feature | Reason |
|---|---|
| Admin Panel UI | Outside end-user scope; only API token used. |
| Real Payment Processing | Demo site does not support live transactions. |
| Email Notifications | Cannot verify outbound emails on demo environment. |
| Mobile Responsiveness | Out of scope for this phase. |
| Database Layer | Requires local setup; planned for future phase. |
| SEO / Accessibility | Out of scope for this phase. |

---

## 7. Test Types

### 7.1 Manual Testing
- Exploratory testing to understand application behaviour.
- Test case execution and defect logging.
- Covers all 3 modules across positive, negative, and edge case scenarios.

### 7.2 UI & Functional Automation (Cypress)
- Automates all manual test cases post-execution.
- Framework: **Page Object Model + Custom Commands**.
- Covers happy paths, negative flows, and form validations.
- Integrated with **GitHub Actions** for CI on every push.

### 7.3 API Testing
- **Postman:** Standalone API collection with environment variables, pre-request scripts, and assertions
- **Cypress `cy.request()`:** API tests co-located with UI tests for integrated coverage.
- Covers: login token, cart CRUD, order creation.

### 7.4 Performance Testing (JMeter)
- Executed against **local OpenCart instance** (Docker).
- Scenarios: login load, product search under concurrent users, cart add at scale.
- Deliverable: HTML JMeter report with response time, throughput, error rate.

---

## 8. Tools & Environment

### Application Under Test

| Property | Value |
|---|---|
| Application | OpenCart E-Commerce |
| Environment | Demo — https://demo.opencart.com |
| Admin Credentials | demo / demo |
| Reset Frequency | Periodic (demo data may reset) |
| Local (JMeter) | Docker — bitnami/opencart |

### Tools

| Tool | Purpose | Version |
|---|---|---|
| Cypress | UI & functional automation | Latest |
| Postman | API testing & collections | Latest |
| Newman | Postman CLI runner | Latest |
| JMeter | Performance / load testing | 5.x |
| GitHub Actions | CI/CD pipeline | — |
| Microsoft Excel | Manual test cases, RTM, bug report | — |
| GitHub Issues | Defect tracking | — |

### Browser Coverage

| Browser | Priority |
|---|---|
| Chrome | Primary |
| Firefox | Secondary |
| Edge | Optional |

---

## 9. Entry & Exit Criteria

### Entry Criteria (before testing begins)
- Test plan reviewed and approved.
- Test cases written and reviewed.
- Application accessible on demo environment.
- Cypress project initialized and smoke test passing.
- Postman collection skeleton created.

### Exit Criteria (testing is complete when)
- All planned test cases executed.
- All High and Critical defects resolved or acknowledged.
- Test execution report generated.
- Automation suite passing in CI (GitHub Actions green).
- JMeter report generated with acceptable thresholds.
- RTM updated with final pass/fail status.

---

## 10. Test Deliverables

| Deliverable | Description | Location |
|---|---|---|
| Test Plan | This document | `manual-testing/Test_Plan.md` |
| Test Cases | Excel sheet with all scenarios | `manual-testing/Test_Cases_OpenCart.xlsx` |
| RTM | Requirement Traceability Matrix | `manual-testing/RTM.xlsx` |
| Bug Report | Defect log with severity & steps | `manual-testing/Bug_Report.xlsx` |
| Cypress Suite | Automated UI + API tests | `cypress/e2e/` |
| Postman Collection | API test collection + environment | `postman/` |
| JMeter Test Plan | Load test scripts | `jmeter/` |
| CI Pipeline | GitHub Actions workflow | `.github/workflows/` |
| README | Full project documentation | `README.md` |

---

## 11. Roles & Responsibilities

| Role | Responsibility |
|---|---|
| QA Engineer | Test planning, test case design, manual execution, automation development, defect logging, reporting. |
| Application Owner | OpenCart open-source community. |
| Reviewer |  Any open-source contributor or developer viewing the public repository. |

---

## 12. Risks & Mitigations

| # | Risk | Impact | Probability | Mitigation |
|---|---|---|---|---|
| 1 | Demo site resets and wipes test data | High | Medium | Re-create test accounts before each run; use `cy.session()` for login caching |
| 2 | Demo site is down or slow | High | Low | Schedule testing during off-peak hours; use local Docker for critical runs |
| 3 | Selectors change after demo update | Medium | Low | Use stable attributes (`id`, `name`) over fragile CSS paths; review after each visit |
| 4 | API endpoints differ from documentation | Medium | Medium | Discover endpoints via browser Network tab; document findings in Postman |
| 5 | Load testing impacts shared demo environment | High | High | Never run JMeter against demo.opencart.com — always use local Docker instance |

---

## 13. Schedule

| Phase | Activity | Duration |
|---|---|---|
| Phase 0 | Project setup, repo structure, tool installation | Day 1 |
| Phase 1 | Manual test case writing (all 3 modules) | Day 2–4 |
| Phase 2 | Manual test execution + bug logging | Day 5–6 |
| Phase 3 | Cypress POM + Custom Commands setup | Day 7 |
| Phase 4 | Cypress UI automation — Search & Cart | Day 8–9 |
| Phase 5 | Cypress UI automation — Checkout & Wishlist | Day 10–11 |
| Phase 6 | API testing — Postman + cy.request() | Day 12–13 |
| Phase 7 | JMeter performance testing (local) | Day 14–15 |
| Phase 8 | GitHub Actions CI + final cleanup | Day 16 |
| Phase 9 | README polish | Day 17 |

---

## 14. Assumptions & Dependencies

- The OpenCart demo site remains accessible throughout the testing period.
- Demo site behaviour is consistent enough for repeatable test execution.
- No backend or database access is available on the live demo environment.
- JMeter load testing will only be performed on a locally hosted OpenCart instance.
- Test user accounts may need to be re-registered if the demo resets.
- All automation will be written in JavaScript (Cypress).
- GitHub will be used for version control and CI/CD.

---

*Document prepared as part of the OpenCart QA Suite portfolio project.*  
*Last updated: March 2026*