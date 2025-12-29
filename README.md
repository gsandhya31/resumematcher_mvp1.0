# Resume-JD Matcher

AI-powered tool to analyze resume alignment with job descriptions and provide actionable insights for job seekers.

Link (MVP1.0-earlier version) : https://resume-sparkle-uploade.lovable.app/
	•	Watch my 90-second walkthrough: https://youtu.be/VM36UPzr5vg 

## 🎯 Product Overview

**Problem:** Job seekers struggle to tailor resumes to specific roles. They don't know which skills to emphasize, which critical skills they're missing, or how to strengthen weak representations.

**Solution:** Resume-JD Matcher uses AI to intelligently compare resumes against job descriptions, providing:
- Matched skills with evidence and confidence levels
- Weakly represented skills with specific improvement guidance
- Critical missing must-have requirements
- Nice-to-have optional skills for prioritization

**Impact:** Helps users optimize resumes for specific roles, increasing interview chances by clearly showing skill gaps and improvement areas.

---

## ✨ Key Features

### 1. Intelligent Skill Matching
- **Semantic understanding**: Recognizes "React.js" = "React" = "ReactJS"
- **Strict technical matching**: Distinguishes C ≠ C++, Java ≠ JavaScript
- **Evidence-based**: Every match includes direct quote from resume
- **Confidence scoring**: High/Medium/Low based on strength of evidence

### 2. Weak Skill Detection
- Identifies skills mentioned without depth
- Explains why representation is weak
- Provides actionable improvement guidance
- Example: "Worked with AWS" → flagged as weak without specific services/achievements

### 3. Smart Categorization
- **Must-have missing**: Critical requirements from JD
- **Optional missing**: Nice-to-have skills for prioritization
- **Experience requirements**: Automatically extracts and flags years of experience gaps

### 4. Real-time Analysis
- Processing time: < 15 seconds
- Progress indicators with 3-step loading animation
- Mobile-responsive design

---

## 🛠️ Technical Stack

### Frontend
- **Framework**: React with TypeScript
- **Styling**: Tailwind CSS
- **Build Tool**: Vite
- **Development**: Lovable (AI-powered development platform)
- **UI Components**: Shadcn/ui, Lucide React icons

### Backend
- **Platform**: Supabase Edge Functions (Serverless)
- **Runtime**: Deno
- **API Integration**: OpenAI GPT-4o

### AI/ML
- **Model**: OpenAI GPT-4o
- **Approach**: Prompt engineering with structured JSON output
- **Temperature**: 0 (deterministic results)
- **Cost per analysis**: ~$0.30

### Deployment
- **Frontend**: Vercel
- **Backend**: Supabase
- **Version Control**: GitHub
- **CI/CD**: Automatic deployment via GitHub integration

---

## 🏗️ Architecture

### Data Flow
```
User Upload (Resume PDF + JD Text)
         ↓
Frontend (React) - File parsing & validation
         ↓
Supabase Edge Function - API orchestration
         ↓
OpenAI GPT-4o - Skill analysis with custom prompts
         ↓
Response Transformation - Structure data for UI
         ↓
Frontend Display - 4-section results view
```

### Key Design Decisions

**1. Single API Call vs Pipeline**
- **Decision**: Single API call with comprehensive prompt
- **Rationale**: Faster MVP iteration, lower latency, sufficient accuracy for 90%+ cases
- **Trade-off**: Slightly less modular than 4-call pipeline, but 3x faster

**2. Model Selection: GPT-4o-mini → GPT-4o**
- **Initial**: Started with GPT-4o-mini ($0.10/analysis)
- **Testing revealed**: 80% accuracy on must-have/optional categorization
- **Upgrade to GPT-4o**: 90-95% accuracy, 3x cost but critical for credibility
- **Business justification**: $15 vs $5 for 50 demos is negligible; accuracy matters

**3. Prompt Engineering Strategy**
- **Rule-based + AI**: Explicit rules for language matching (C++ ≠ C) + AI for semantic understanding
- **Structured output**: Force JSON format with validation
- **Evidence requirement**: Every match must quote resume text (reduces hallucinations)

---

## 🚀 Getting Started

### Prerequisites
- Node.js 18+ 
- Supabase account
- OpenAI API key

### Installation
```bash
# Clone repository
git clone https://github.com/yourusername/resume-jd-matcher.git
cd resume-jd-matcher

# Install dependencies
npm install

# Set up environment variables
cp .env.example .env
# Add your OpenAI API key to .env

# Run locally
npm run dev
```

### Supabase Setup
```bash
# Install Supabase CLI
npm install -g supabase

# Link to your project
supabase link --project-ref your-project-ref

# Deploy edge function
supabase functions deploy analyze-resume

# Set OpenAI API key as secret
supabase secrets set OPENAI_API_KEY=your-key-here
```

---

## 📊 Testing

### Synthetic Test Cases

Four comprehensive test cases validate edge cases:

**Test 1: Semantic Matching**
- Resume: "React.js developer"
- JD: "React required"
- Expected: Match (not missing)

**Test 2: Strict Language Matching**
- Resume: "C++ expert"
- JD: "C programming required"
- Expected: C++ matched, C in missing

**Test 3: Categorization Accuracy**
- JD: "Docker required, Kubernetes nice-to-have"
- Expected: Correct must-have vs optional distinction

**Test 4: Weak Skill Detection**
- Resume: "Worked with AWS"
- Expected: Flagged as weak with specific reason

### Running Tests
```bash
# Run with sample data
npm run test:sample

# Test individual cases
npm run test:case1
npm run test:case2
npm run test:case3
npm run test:case4
```

---

## 🎤 Product Management Approach

### PRD & User Stories
- Started with comprehensive PRD defining scope, goals, and out-of-scope items
- Decomposed into 9 user stories across 3 epics
- Prioritized MVP features: skill matching first, rewrite suggestions later

### Iterative Development
- Built core matching (US 4-7) before enhancement features (US 8-9)
- Tested with synthetic data before real resumes
- Iterated based on testing feedback (model upgrade, years extraction)

### Data-Driven Decisions
- Testing revealed GPT-4o-mini insufficient accuracy
- Evidence: Kubernetes miscategorization, Java test failure
- Decision: Upgrade to GPT-4o based on data, not assumptions

### Key Insights
1. **Don't prematurely optimize**: Started with cheaper model, validated need for upgrade
2. **Test edge cases early**: Synthetic tests caught issues before production
3. **User-centric design**: Four-section results for clear actionability
4. **Technical depth matters**: Understanding LLM capabilities informed architecture

---

## 🗺️ Roadmap

### Phase 1: MVP (Current) ✅
- [x] Resume upload & JD input
- [x] Skill matching with evidence
- [x] Must-have vs optional categorization
- [x] Weak skill detection
- [x] Years of experience extraction

### Phase 2: Enhancement (Next)
- [ ] Rewrite suggestions for weak skills (US-8)
- [ ] Experience level tone adjustment (US-9)
- [ ] Loading time optimization (8s → 5s)

### Phase 3: Advanced Features
- [ ] ATS keyword optimization score
- [ ] Multiple resume version comparison
- [ ] Export results as PDF report
- [ ] Historical tracking & analytics

### Phase 4: Scale & Polish
- [ ] User authentication
- [ ] Resume history storage
- [ ] Chrome extension for auto-fill
- [ ] LinkedIn integration

---

## 📈 Success Metrics

### Input Quality
- Parsing accuracy: 95%+ for PDF text extraction
- JD understanding: Manual review of 100 analyses

### Output Quality
- Skill matching accuracy: 90-95% (human review benchmark)
- False positive rate: < 5%
- False negative rate: < 10%

### User Value
- Actionability: % users updating resume after analysis
- Interview rate: Track 30 days before/after usage
- NPS: Post-analysis survey

### Business Metrics
- Cost per analysis: $0.30 (GPT-4o)
- Processing time: < 15 seconds p95
- Error rate: < 1% API failures

---


---

## 📄 License

This project is licensed under the MIT License - see [LICENSE](LICENSE) file for details.

---

## 👤 Author

**[Sandhya G]**
- Portfolio: 
- LinkedIn: (https://www.linkedin.com/in/sandhya-godavarthy-5072622b/)
- Email: gsandhya31@gmail.com

---

## 🙏 Acknowledgments

- OpenAI for GPT-4o API
- Supabase for serverless infrastructure
- Lovable for rapid development platform
- Shadcn/ui for component library

---

## 📞 Contact & Feedback

Questions or feedback? 
- Open an issue: [GitHub Issues](https://github.com/yourusername/resume-jd-matcher/issues)
- Email: your.email@example.com
- Twitter: [@yourhandle]

---

**Built with ❤️ to showcase AI Product Management skills**
```
