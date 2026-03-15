# Test Plan — amitnath-lab/amitnath-lab

## Overview

This test plan covers the two commits (treated as merged changes) in this repository:

| # | Commit SHA | Message | Date |
|---|-----------|---------|------|
| 1 | `363c001` | Initial commit | 2023-07-03 |
| 2 | `1d9528a` | Update README.md | 2023-07-03 |

**File under test:** `README.md`

---

## Test Suite Structure

```
tests/
  readme/
    TC-001_html_structure.test
    TC-002_heading_content.test
    TC-003_personal_info.test
    TC-004_social_links.test
    TC-005_tech_stack_links.test
    TC-006_tech_stack_images.test
    TC-007_link_reachability.test
    TC-008_accessibility.test
    TC-009_template_removal.test
```

---

## Test Cases

### TC-001 — HTML Structure Validation

**PR/Commit:** `1d9528a` (Update README.md)
**Category:** Static Analysis
**Automation Tool:** `html-validator`, `cheerio`, or `rehype`

| Field | Value |
|-------|-------|
| Test ID | TC-001 |
| Title | README.md contains valid HTML structure |
| Type | Static / Lint |
| Priority | High |

**Steps:**
1. Read `README.md` file content
2. Parse all inline HTML elements
3. Validate each tag is properly opened and closed

**Assertions:**
```yaml
- assert: all_html_tags_are_closed
- assert: no_malformed_attributes
- assert: img_tags_have_alt_attribute
- assert: anchor_tags_have_href_attribute
```

---

### TC-002 — Heading Content Verification

**PR/Commit:** `1d9528a` (Update README.md)
**Category:** Content
**Automation Tool:** `cheerio`, `marked`, regex

| Field | Value |
|-------|-------|
| Test ID | TC-002 |
| Title | H1 and H3 headings contain correct profile content |
| Type | Content / Functional |
| Priority | High |

**Steps:**
1. Parse `README.md` as HTML
2. Extract all `<h1>` and `<h3>` elements

**Assertions:**
```yaml
- assert: h1_exists
  selector: "h1[align='center']"
  contains: "Hi"
  contains: "I'm Amit"

- assert: h3_bio_exists
  selector: "h3[align='center']"
  contains: "enterprise architect"
  contains: "digital transformations"
  contains: "ecommerce"

- assert: h3_connect_exists
  selector: "h3[align='left']"
  contains: "Connect with me"

- assert: h3_tools_exists
  selector: "h3[align='left']"
  contains: "Languages and Tools"
```

---

### TC-003 — Personal Information Content

**PR/Commit:** `1d9528a` (Update README.md)
**Category:** Content
**Automation Tool:** regex, `fs.readFileSync`

| Field | Value |
|-------|-------|
| Test ID | TC-003 |
| Title | Personal info bullet points render with correct data |
| Type | Content |
| Priority | High |

**Steps:**
1. Read raw `README.md` text
2. Match each expected bullet point

**Assertions:**
```yaml
- assert: contains_medium_link
  pattern: "https://medium.com/@amitnath"

- assert: contains_expertise_keywords
  keywords:
    - "CommerceTools"
    - "SAP Commerce"
    - "micro-services"
    - "Adobe Experience Manager"
    - "AEM"
    - "AWS"
    - "Azure"
    - "Kubernetes"
    - "Terraform"
    - "Terragrunt"
    - "Ansible"
    - "Forgerock"
    - "Auth0"
    - "Keycloak"
    - "Cognito"

- assert: contains_email
  pattern: "amit_knath@live.com"

- assert: contains_linkedin_profile
  pattern: "https://www.linkedin.com/in/amit-knath/"

- assert: contains_fun_fact
  pattern: "No success yet with trading robots"
```

---

### TC-004 — Social Links Section

**PR/Commit:** `1d9528a` (Update README.md)
**Category:** Links / Integration
**Automation Tool:** `cheerio`, Playwright, or Cypress

| Field | Value |
|-------|-------|
| Test ID | TC-004 |
| Title | Social media links render with correct href and image |
| Type | Functional |
| Priority | High |

**Steps:**
1. Parse HTML in `README.md`
2. Find the "Connect with me" section
3. Extract all `<a>` tags and their nested `<img>` tags

**Assertions:**
```yaml
- assert: linkedin_link_exists
  selector: "a[href='https://linkedin.com/in/amit-knath']"
  attributes:
    target: "blank"
  child_img:
    alt: "amit-knath"
    height: "30"
    width: "40"

- assert: medium_link_exists
  selector: "a[href='https://medium.com/amitnath']"
  attributes:
    target: "blank"
  child_img:
    alt: "amitnath"
    height: "30"
    width: "40"
```

---

### TC-005 — Tech Stack Links (href Attributes)

**PR/Commit:** `1d9528a` (Update README.md)
**Category:** Links
**Automation Tool:** `cheerio`, regex

| Field | Value |
|-------|-------|
| Test ID | TC-005 |
| Title | All technology links in "Languages and Tools" have valid hrefs |
| Type | Functional / Static |
| Priority | Medium |

**Steps:**
1. Parse the "Languages and Tools" `<p>` block
2. Extract all `<a>` tags with `target="_blank"`
3. Validate each href is a well-formed HTTPS URL

**Expected technologies and their URLs:**
```yaml
tech_links:
  - name: aws
    href: "https://aws.amazon.com"
  - name: azure
    href: "https://azure.microsoft.com/en-in/"
  - name: babel
    href: "https://babeljs.io/"
  - name: bash
    href: "https://www.gnu.org/software/bash/"
  - name: bootstrap
    href: "https://getbootstrap.com"
  - name: docker
    href: "https://www.docker.com/"
  - name: express
    href: "https://expressjs.com"
  - name: figma
    href: "https://www.figma.com/"
  - name: gatsby
    href: "https://www.gatsbyjs.com/"
  - name: git
    href: "https://git-scm.com/"
  - name: graphql
    href: "https://graphql.org"
  - name: java
    href: "https://www.java.com"
  - name: javascript
    href: "https://developer.mozilla.org/en-US/docs/Web/JavaScript"
  - name: jenkins
    href: "https://www.jenkins.io"
  - name: kotlin
    href: "https://kotlinlang.org"
  - name: kubernetes
    href: "https://kubernetes.io"
  - name: linux
    href: "https://www.linux.org/"
  - name: mongodb
    href: "https://www.mongodb.com/"
  - name: mssql
    href: "https://www.microsoft.com/en-us/sql-server"
  - name: mysql
    href: "https://www.mysql.com/"
  - name: nextjs
    href: "https://nextjs.org/"
  - name: nginx
    href: "https://www.nginx.com"
  - name: nodejs
    href: "https://nodejs.org"
  - name: oracle
    href: "https://www.oracle.com/"
  - name: pandas
    href: "https://pandas.pydata.org/"
  - name: python
    href: "https://www.python.org"
  - name: react
    href: "https://reactjs.org/"
  - name: reactnative
    href: "https://reactnative.dev/"
  - name: redis
    href: "https://redis.io"
  - name: solr
    href: "https://lucene.apache.org/solr/"
  - name: spring
    href: "https://spring.io/"
  - name: tensorflow
    href: "https://www.tensorflow.org"
  - name: typescript
    href: "https://www.typescriptlang.org/"
  - name: vuejs
    href: "https://vuejs.org/"
  - name: webpack
    href: "https://webpack.js.org"

assertions:
  - all_hrefs_start_with_https
  - all_links_have_rel_noreferrer
  - all_links_have_target_blank
  - total_link_count: 35
```

---

### TC-006 — Tech Stack Icon Images

**PR/Commit:** `1d9528a` (Update README.md)
**Category:** Content / Static
**Automation Tool:** `cheerio`

| Field | Value |
|-------|-------|
| Test ID | TC-006 |
| Title | Every technology icon image has correct alt, width=40, height=40 |
| Type | Content |
| Priority | Medium |

**Steps:**
1. Parse all `<img>` tags inside the Languages and Tools `<p>` block
2. Validate attributes for each

**Assertions:**
```yaml
- assert: every_img_has_alt_text
- assert: every_img_width_equals_40
- assert: every_img_height_equals_40
- assert: every_img_src_is_absolute_url
- assert: total_image_count: 35
```

---

### TC-007 — External Link Reachability (Integration)

**PR/Commit:** `1d9528a` (Update README.md)
**Category:** Integration / E2E
**Automation Tool:** `node-fetch`, Playwright, or `link-checker`

| Field | Value |
|-------|-------|
| Test ID | TC-007 |
| Title | All external URLs in README respond with HTTP 2xx |
| Type | Integration |
| Priority | Low (network-dependent) |

**Steps:**
1. Extract all unique URLs from `README.md`
2. HTTP GET each URL
3. Assert response status is 200–299

**Assertions:**
```yaml
- assert: all_urls_return_2xx
  timeout_ms: 5000
  retry: 2
  exclude_pattern: "raw.githubusercontent.com"  # CDN; optionally skip
```

---

### TC-008 — Accessibility Checks

**PR/Commit:** `1d9528a` (Update README.md)
**Category:** Accessibility
**Automation Tool:** `axe-core`, `pa11y`

| Field | Value |
|-------|-------|
| Test ID | TC-008 |
| Title | README HTML passes basic accessibility rules |
| Type | Accessibility |
| Priority | Low |

**Assertions:**
```yaml
- assert: all_images_have_non_empty_alt
- assert: links_have_discernible_text_or_image_alt
- assert: no_duplicate_link_text_pointing_to_different_hrefs
```

---

### TC-009 — Template Boilerplate Removed

**PR/Commit:** `1d9528a` (Update README.md)
**Category:** Regression
**Automation Tool:** `fs.readFileSync`, regex

| Field | Value |
|-------|-------|
| Test ID | TC-009 |
| Title | Original GitHub profile template placeholder text does not exist |
| Type | Regression |
| Priority | High |

**Steps:**
1. Read `README.md` raw text

**Assertions (these strings must NOT be present):**
```yaml
- assert_not_present: "### Hi there"
- assert_not_present: "I'm currently working on ..."
- assert_not_present: "I'm currently learning ..."
- assert_not_present: "I'm looking to collaborate on ..."
- assert_not_present: "I'm looking for help with ..."
- assert_not_present: "Pronouns: ..."
- assert_not_present: "<!--"
- assert_not_present: "-->"
```

---

## Summary Table

| Test ID | Title | Priority | Type | Tool Suggestion |
|---------|-------|----------|------|----------------|
| TC-001 | HTML structure validation | High | Static | `cheerio` / `html-validator` |
| TC-002 | Heading content verification | High | Content | `cheerio` |
| TC-003 | Personal information content | High | Content | `regex` / `fs` |
| TC-004 | Social links section | High | Functional | `cheerio` |
| TC-005 | Tech stack links (href attributes) | Medium | Functional | `cheerio` |
| TC-006 | Tech stack icon images | Medium | Content | `cheerio` |
| TC-007 | External link reachability | Low | Integration | `node-fetch` |
| TC-008 | Accessibility checks | Low | Accessibility | `axe-core` / `pa11y` |
| TC-009 | Template boilerplate removed | High | Regression | `regex` / `fs` |

---

## Recommended Automation Stack

```json
{
  "language": "JavaScript / TypeScript",
  "test_runner": "Jest or Vitest",
  "html_parser": "cheerio",
  "link_checker": "node-fetch",
  "accessibility": "axe-core",
  "ci": "GitHub Actions"
}
```

### Sample Jest Test File Structure

```javascript
// tests/readme.test.js
const fs = require('fs');
const cheerio = require('cheerio');

const README = fs.readFileSync('./README.md', 'utf8');
const $ = cheerio.load(README);

describe('TC-001: HTML Structure', () => {
  test('img tags have alt attribute', () => {
    $('img').each((_, el) => {
      expect($(el).attr('alt')).toBeTruthy();
    });
  });
});

describe('TC-002: Heading Content', () => {
  test('H1 contains profile name', () => {
    expect($('h1').text()).toContain("I'm Amit");
  });
  test('H3 bio contains enterprise architect', () => {
    expect($('h3[align="center"]').text()).toContain('enterprise architect');
  });
});

describe('TC-003: Personal Information', () => {
  test('Contains Medium link', () => {
    expect(README).toContain('https://medium.com/@amitnath');
  });
  test('Contains email', () => {
    expect(README).toContain('amit_knath@live.com');
  });
  test('Contains LinkedIn', () => {
    expect(README).toContain('https://www.linkedin.com/in/amit-knath/');
  });
  test('Contains fun fact', () => {
    expect(README).toContain('No success yet with trading robots');
  });
});

describe('TC-005: Tech Stack Links', () => {
  test('All tech links use HTTPS', () => {
    const links = $('p a[target="blank"], p a[target="_blank"]');
    links.each((_, el) => {
      const href = $(el).attr('href');
      expect(href).toMatch(/^https?:\/\//);
    });
  });
});

describe('TC-006: Tech Stack Images', () => {
  test('All tech icons are 40x40', () => {
    $('p a img').each((_, el) => {
      expect($(el).attr('width')).toBe('40');
      expect($(el).attr('height')).toBe('40');
    });
  });
});

describe('TC-009: Template Boilerplate Removed', () => {
  const placeholders = [
    "### Hi there",
    "I'm currently working on ...",
    "I'm currently learning ...",
    "<!--",
  ];
  placeholders.forEach(text => {
    test(`Does not contain "${text}"`, () => {
      expect(README).not.toContain(text);
    });
  });
});
```
