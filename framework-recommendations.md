# Compliance Framework Recommendations

## Scenario A: Medisync (HealthTech)

**Recommended framework(s):** HIPAA, SOC 2 Type II, CIS AWS Foundations Benchmark

**Why these frameworks:**
Medisync is a US-based telemedicine company handling patient medical records, prescriptions, and appointment history, so HIPAA is the primary legal and regulatory driver because it applies to protected health information (PHI). SOC 2 Type II is also valuable because hospitals, clinics, and investors will want independent assurance that security controls are designed and operating effectively. CIS AWS Foundations Benchmark is a practical technical baseline for securing their AWS environment and supports the broader HIPAA/SOC 2 roadmap.

**Starting point:**
Start with HIPAA-aligned security and privacy controls first, because handling patient data creates immediate legal and business risk. In parallel, use CIS AWS Foundations Benchmark as the technical baseline, then work toward SOC 2 Type II as the company matures and needs stronger trust signals for customers and investors.

---

## Scenario B: Flowdock (B2B SaaS for EU)

**Recommended framework(s):** ISO/IEC 27001, SOC 2 Type II, GDPR-aligned security/privacy controls

**Why these frameworks:**
Flowdock sells to large French and German enterprises, and procurement teams in Europe commonly ask for formal certifications, making ISO 27001 the strongest fit because it is widely recognized internationally. SOC 2 Type II is also useful for enterprise SaaS buyers, especially for demonstrating operational security controls. Because the company is expanding into Europe and serving EU-based customers, it must also align its security and privacy practices with GDPR requirements, even though GDPR is a regulation rather than a certification framework.

**Starting point:**
Start with ISO 27001 because it directly answers the enterprise procurement question, “What certifications do you have?” Then build toward SOC 2 Type II to strengthen assurance for a broader range of customers, while making sure GDPR-related privacy and data handling requirements are addressed throughout.

---

## Scenario C: Spendwise (Fintech, early stage)

**Recommended framework(s):** CIS AWS Foundations Benchmark, NIST Cybersecurity Framework (CSF), SOC 2 Type II

**Why these frameworks:**
Spendwise is a very early-stage fintech startup with only 3 engineers and 3 months to establish a basic security baseline, so they need something practical and fast to implement. CIS AWS Foundations Benchmark gives them concrete AWS hardening steps, while NIST CSF provides a simple structure for organizing their security program across identify, protect, detect, respond, and recover. SOC 2 Type II is likely important later as the company grows and needs to prove trustworthiness to partners, investors, and customers.

**Starting point:**
Start with CIS AWS Foundations Benchmark first because it is the fastest way to establish a minimum security baseline in AWS. Then use NIST CSF to organize the broader security program, and pursue SOC 2 once the core controls are in place and the company is ready for external attestation.
