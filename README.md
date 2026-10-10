<<<<<<< HEAD
# React + Vite

This template provides a minimal setup to get React working in Vite with HMR and some ESLint rules.

Currently, two official plugins are available:

- [@vitejs/plugin-react](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react) uses [Oxc](https://oxc.rs)
- [@vitejs/plugin-react-swc](https://github.com/vitejs/vite-plugin-react/blob/main/packages/plugin-react-swc) uses [SWC](https://swc.rs/)

## React Compiler

The React Compiler is not enabled on this template because of its impact on dev & build performances. To add it, see [this documentation](https://react.dev/learn/react-compiler/installation).

## Expanding the ESLint configuration

If you are developing a production application, we recommend using TypeScript with type-aware lint rules enabled. Check out the [TS template](https://github.com/vitejs/vite/tree/main/packages/create-vite/template-react-ts) for information on how to integrate TypeScript and [`typescript-eslint`](https://typescript-eslint.io) in your project.
=======
# MatchProof AI — Evidence-Backed Ad Auditor

**Verify advertising promises against landing-page evidence.**

MatchProof AI is an AI-assisted advertising audit MVP that helps identify claims in advertisements that may lack sufficient support in their destination landing-page content. It provides a message-match score, claim-level findings, explanations, and recommended fixes.

The project emphasizes evidence-based analysis and responsible reporting: missing evidence does not automatically mean an advertising claim is false.

## 1. Problem Statement

Advertisements often promise specific benefits, offers, discounts, or outcomes. However, the destination landing page may not clearly support those promises.

Manually checking every advertisement against its landing page can be time-consuming. MatchProof AI helps identify potential inconsistencies and presents findings that advertisers can review.

## 2. Key Features

- **Ad claim analysis:** Accepts advertisement copy and landing-page text.
- **Message-match scoring:** Generates a heuristic score to summarize the analysis.
- **Claim-level findings:** Classifies claims as potentially supported, missing support, or potentially contradicted.
- **Evidence-aware reporting:** Provides explanations and supporting evidence when available.
- **Recommended fixes:** Suggests ways to substantiate claims or revise advertisement copy.
- **Inaccessible-page handling:** Handles recorded HTTP 404 responses without assigning a misleading score.
- **Input validation:** Requires advertisement text and landing-page text for normal analysis.
- **API integration:** Connects the frontend to a Python FastAPI backend.

## 3. Technology Stack

| Component | Technology |
|---|---|
| Frontend | React, TypeScript |
| Frontend development | Lovable |
| Backend API | Python, FastAPI |
| API server | Uvicorn |
| HTML parsing dependency | Beautiful Soup 4 |
| Automated testing | Pytest, FastAPI TestClient |
| HTTP testing dependency | HTTPX |
| Version control | Git and GitHub |

## 4. System Architecture

The application follows a frontend-backend architecture.

1. The user enters advertisement text and destination landing-page text.
2. The frontend sends the input to the FastAPI `/analyze` endpoint.
3. The backend analyzes the supplied content and produces structured results.
4. The frontend displays the score, claim findings, explanations, and recommended fixes.
5. If the request contains a recorded HTTP 404 status, the backend returns an inaccessible-page result without calculating a message-match score.

## 5. Project Structure

```text
hackathon-psg/
├── backend/
│   ├── main.py
│   ├── requirements.txt
│   └── tests/
│       └── test_inaccessible_page.py
├── .gitignore
└── README.md
```

The frontend is developed using Lovable and may be maintained separately from the backend repository.

## 6. Prerequisites

Install the following before running the backend:

- Python 3.10 or later
- pip
- Git
- A modern web browser

## 7. Backend Setup

Clone the repository:

```bash
git clone https://github.com/Hariharan-VS-18/hackathon-psg.git
cd hackathon-psg
```

Create a virtual environment:

```bash
python -m venv .venv
```

Activate it on Windows PowerShell:

```powershell
.\.venv\Scripts\Activate.ps1
```

Install dependencies:

```bash
python -m pip install -r backend/requirements.txt
```

Start the FastAPI server from the project root:

```bash
python -m uvicorn backend.main:app --reload
```

The local API is available at:

`http://127.0.0.1:8000`

Interactive API documentation:

`http://127.0.0.1:8000/docs`

Keep the terminal running while using the local API.

## 8. API Usage

### Endpoint

`POST /analyze`

Local URL:

`http://127.0.0.1:8000/analyze`

### Example request — Normal analysis

```json
{
  "ad_text": "Get same-day approval.",
  "landing_page_text": "Apply online for account approval."
}
```

The response includes analysis information such as the message-match score, number of claims analyzed, finding counts, explanations, and recommended fixes.

The score is heuristic and should not be interpreted as a statistically validated measure of advertising accuracy.

### Example request — Recorded HTTP 404

```json
{
  "ad_text": "Get approved on the same day.",
  "destination_url": "https://example.com/offer",
  "http_status": 404
}
```

Expected response behavior:

- `page_status`: `inaccessible`
- `http_status`: `404`
- `score`: `null`
- `score_status`: `unavailable`
- `findings`: empty array
- `evidence_quotes`: empty array

The response message is:

**Landing page inaccessible — unable to assess message match.**

The HTTP 200 returned by this API request indicates that the analysis request was handled successfully. It does not mean the destination page itself returned HTTP 200.

## 9. Running Automated Tests

Run the inaccessible-page test from the project root:

```bash
python -m pytest backend/tests/test_inaccessible_page.py -v
```

The test verifies that a recorded 404 response produces an inaccessible-page status, a null score, and no fabricated findings or evidence.

## 10. Frontend

The MatchProof AI frontend provides:

- Advertisement and landing-page text inputs
- Optional destination URL input
- An inaccessible-page test toggle
- An analysis button
- Message-match score and claim statistics
- Claim-level findings and severity indicators
- Explanations and recommended fixes
- Input validation and error messaging

The frontend sends requests to the FastAPI backend and displays the returned analysis.

For local development, the frontend must be able to reach the backend URL. If the frontend is hosted remotely, a deployed, reachable backend endpoint is required; a local `127.0.0.1` address is not accessible to remote visitors.

## 11. Responsible AI and Limitations

MatchProof AI is a decision-support tool, not a legal determination or a guarantee of advertising compliance.

- Missing supporting evidence does not prove that a claim is false.
- A potentially contradicted claim should be distinguished from a claim with missing support.
- Evidence quotes must correspond to the supplied landing-page content.
- The message-match score is heuristic and has not been independently validated.
- The current inaccessible-page flow handles a recorded HTTP status; automatic live URL inspection is not claimed as implemented.
- Analysis quality depends on the completeness and accuracy of the supplied content.

## 12. Future Improvements

- Automated and secure landing-page URL inspection
- Support for offline HTML snapshots and additional content formats
- Improved semantic claim-to-evidence matching
- Evaluation against manually verified examples
- Evidence highlighting and downloadable audit reports
- Batch analysis of multiple advertisements
- Deployment of the frontend and backend for public access

## 13. Team and Contribution

MatchProof AI was developed collaboratively by a three-member hackathon team.

### Member 1 — Frontend Development
- Designed and developed the MatchProof AI dashboard using Lovable and React.
- Implemented advertisement and landing-page input forms.
- Integrated the frontend with the FastAPI backend.
- Displayed analysis scores, claim findings, recommendations, and inaccessible-page messages.

### Member 2 — Backend Development
- Developed the FastAPI backend and analysis endpoint.
- Implemented structured claim-analysis responses.
- Added handling for recorded HTTP 404 responses.
- Implemented automated tests for inaccessible-page scenarios.
- Verified API behavior and frontend-backend communication.

### Member 3 — Testing, Evaluation and Integration
- Completed dataset inspection and test-case preparation.
- Verified claim findings and evidence against supplied landing-page content.
- Tested analysis scenarios and helped identify potential false positives.
- Completed assigned evaluation and integration tasks.
- Contributed to project validation and MVP readiness.

### Team Outcome
All three members completed their assigned responsibilities and collaborated to prepare the MatchProof AI MVP for submission.

This project was developed as a hackathon MVP using collaborative frontend and backend development.

The code is maintained in GitHub:

https://github.com/Hariharan-VS-18/hackathon-psg

## Conclusion

MatchProof AI demonstrates an evidence-oriented approach to advertising audits by comparing ad promises with supplied landing-page content, identifying potential gaps, and communicating uncertainty responsibly.

Its core principle is simple: **report what the available evidence supports, and never invent proof.**
>>>>>>> d82c458 (Update team contributions in README)
