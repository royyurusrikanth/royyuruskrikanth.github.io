import { useMemo, useState } from "react";
import { motion } from "framer-motion";
import { BookOpen, GraduationCap, Mail, MapPin, Mic2, Newspaper, ShieldCheck, User, Github, Linkedin, Globe, Phone } from "lucide-react";
import { Card, CardContent, CardHeader, CardTitle } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { Input } from "@/components/ui/input";

// ====== EDIT ME: Basic profile data ======
const profile = {
  name: "Dr. Royyuru Srikanth",
  title: "Assistant/Associate Professor • Machine Learning • Brain Tumor Detection • Cybersecurity",
  email: "royyurusrikanth@gmail.com",
  phone: "+91-9381229528",
  location: "Hyderabad, Telangana, India",
  scholar: "", // add Google Scholar URL
  orcid: "", // add ORCID URL
  github: "https://github.com/royyuruskrikanth",
  linkedin: "", // add LinkedIn URL
  website: "https://royyuruskrikanth.github.io",
};

// ====== EDIT ME: Research interests ======
const interests = [
  "Machine Learning & Deep Learning",
  "Medical Image Analysis (MRI, Brain Tumor)",
  "Survival Time Prediction (Glioblastoma)",
  "Cybersecurity & Cryptography",
  "Cloud Computing & Data Security",
  "Wireless Networks & IoT",
];

// ====== EDIT ME: Quick metrics ======
const metrics = [
  { label: "Teaching Experience", value: "15+ Years" },
  { label: "Publications", value: "20+" },
  { label: "Reviewer / Editor Roles", value: "SN CS • JNS" },
  { label: "UG/PG Projects Guided", value: "40 / 10" },
];

// ====== EDIT ME: Selected publications (add more as needed) ======
const publications = [
  {
    year: 2025,
    title:
      "Segmentation and Classification of Intracranial Tumour Using Machine Learning Techniques",
    venue: "ICIHCNN-2022 (Springer) — Advanced Technologies and Societal Change",
    doi: "10.1007/978-981-99-2832-3",
  },
  {
    year: 2025,
    title:
      "Enhancing Web Security with VulnGuard: An Advanced Vulnerability Scanning Approach",
    venue: "ICETM (IEEE) — DOI: 10.1109/ICETM63734.2025.11051982",
    doi: "10.1109/ICETM63734.2025.11051982",
  },
  {
    year: 2024,
    title:
      "Verifiability and Visibility of the Data Modification in Cloud using Enhanced ABE",
    venue: "ICACC (IEEE) — DOI: 10.1109/ICACC63692.2024.10845454",
    doi: "10.1109/ICACC63692.2024.10845454",
  },
  {
    year: 2024,
    title:
      "Detection & Classification of Brain Tumours with Survival Rate Prediction in Glioblastoma",
    venue: "IJISAE (Scopus)",
    doi: "10.18201/ijisae.v12(14s).pp256-273",
  },
  {
    year: 2024,
    title:
      "Detection of Normal and Abnormal Brain Tumor MRI Images using ML Approaches",
    venue: "Journal of Autonomous Intelligence",
    doi: "10.32629/jai.v7i4.1092",
  },
  {
    year: 2018,
    title:
      "An Emergency Theory of Terminal Relay for WCN with 4G LTE",
    venue: "ICICI-2018 (Springer)",
    doi: "10.1007/978-3-030-03146-6",
  },
];

// ====== EDIT ME: Editorial & reviewer roles ======
const service = [
  {
    role: "Editorial Board Member",
    org: "Journal of Network Security",
  },
  {
    role: "Reviewer",
    org: "SN Computer Science (Springer Nature)",
    note: "Review identifier: 6cc4f791-1d96-4756-b8c2-5c8f5c2628fd",
  },
  {
    role: "Reviewer",
    org: "Various IEEE/Springer conferences & journals",
  },
];

// ====== EDIT ME: Invited talks & session chair ======
const talks = [
  {
    role: "Session Chair / Invited Speaker",
    event: "AI/ML in Healthcare — FDPs & Seminars",
    host: "Multiple Institutions (2020–2025)",
  },
];

// ====== EDIT ME: Teaching portfolio ======
const courses = [
  "Compiler Design",
  "FLAT",
  "Cryptography & Network Security",
  "Design & Analysis of Algorithms",
  "Computer Networks",
  "Data Structures",
];

// ====== Small helpers ======
const Section = ({ id, icon: Icon, title, children }) => (
  <section id={id} className="scroll-mt-24 py-10">
    <div className="max-w-6xl mx-auto px-4">
      <div className="flex items-center gap-3 mb-5">
        <Icon className="w-6 h-6" />
        <h2 className="text-2xl font-semibold">{title}</h2>
      </div>
      {children}
    </div>
  </section>
);

function Pill({ children }) {
  return (
    <span className="px-3 py-1 rounded-full border text-sm">{children}</span>
  );
}

function Metric({ label, value }) {
  return (
    <div className="p-4 rounded-2xl border">
      <div className="text-sm opacity-70">{label}</div>
      <div className="text-xl font-semibold">{value}</div>
    </div>
  );
}

function PubItem({ p }) {
  return (
    <li className="leading-relaxed">
      <span className="font-medium">[{p.year}]</span> {p.title} — <span className="opacity-80">{p.venue}</span>
      {p.doi && (
        <>
          {" "}·{" "}
          <a
            href={`https://doi.org/${p.doi}`}
            className="underline"
            target="_blank"
            rel="noreferrer"
          >
            DOI
          </a>
        </>
      )}
    </li>
  );
}

export default function PortfolioSite() {
  const [query, setQuery] = useState("");

  const filteredPubs = useMemo(() => {
    if (!query) return publications;
    const q = query.toLowerCase();
    return publications.filter(
      (p) =>
        p.title.toLowerCase().includes(q) ||
        p.venue.toLowerCase().includes(q) ||
        String(p.year).includes(q)
    );
  }, [query]);

  return (
    <div className="min-h-screen bg-white text-gray-900">
      {/* Navbar */}
      <div className="sticky top-0 z-40 border-b backdrop-blur bg-white/70">
        <div className="max-w-6xl mx-auto px-4 h-16 flex items-center justify-between">
          <a href="#home" className="font-semibold">{profile.name}</a>
          <nav className="hidden md:flex gap-6 text-sm">
            <a href="#about" className="hover:underline">About</a>
            <a href="#interests" className="hover:underline">Interests</a>
            <a href="#publications" className="hover:underline">Publications</a>
            <a href="#service" className="hover:underline">Service</a>
            <a href="#talks" className="hover:underline">Talks</a>
            <a href="#teaching" className="hover:underline">Teaching</a>
            <a href="#contact" className="hover:underline">Contact</a>
          </nav>
          <div className="flex items-center gap-2">
            <a href={profile.github} target="_blank" rel="noreferrer" className="p-2 rounded-xl border"><Github className="w-4 h-4" /></a>
            {profile.linkedin && (
              <a href={profile.linkedin} target="_blank" rel="noreferrer" className="p-2 rounded-xl border"><Linkedin className="w-4 h-4" /></a>
            )}
            <a href={profile.website} target="_blank" rel="noreferrer" className="p-2 rounded-xl border"><Globe className="w-4 h-4" /></a>
          </div>
        </div>
      </div>

      {/* Hero */}
      <section id="home" className="relative overflow-hidden">
        <div className="max-w-6xl mx-auto px-4 py-14 md:py-24">
          <div className="grid md:grid-cols-3 gap-8 items-center">
            <div className="md:col-span-2">
              <motion.h1
                initial={{ opacity: 0, y: 10 }}
                animate={{ opacity: 1, y: 0 }}
                transition={{ duration: 0.6 }}
                className="text-3xl md:text-5xl font-bold leading-tight"
              >
                {profile.name}
              </motion.h1>
              <p className="mt-3 text-lg opacity-80">{profile.title}</p>
              <div className="mt-6 flex flex-wrap gap-2">
                {metrics.map((m) => (
                  <Metric key={m.label} label={m.label} value={m.value} />
                ))}
              </div>
              <div className="mt-6 flex flex-wrap gap-3">
                <a href="#contact" className="inline-flex items-center gap-2 px-4 py-2 rounded-2xl border">
                  <Mail className="w-4 h-4" /> Contact
                </a>
                <a href="#publications" className="inline-flex items-center gap-2 px-4 py-2 rounded-2xl border">
                  <BookOpen className="w-4 h-4" /> Publications
                </a>
                <a href="#talks" className="inline-flex items-center gap-2 px-4 py-2 rounded-2xl border">
                  <Mic2 className="w-4 h-4" /> Invited Talks
                </a>
              </div>
            </div>
            <div className="md:justify-self-end">
              <div className="w-40 h-40 md:w-52 md:h-52 rounded-2xl border bg-gradient-to-br from-gray-100 to-gray-50 flex items-center justify-center">
                <User className="w-16 h-16 opacity-60" />
              </div>
              <div className="mt-4 text-sm space-y-1">
                <div className="flex items-center gap-2 opacity-80"><MapPin className="w-4 h-4" /> {profile.location}</div>
                <div className="flex items-center gap-2 opacity-80"><Phone className="w-4 h-4" /> {profile.phone}</div>
                <div className="flex items-center gap-2 opacity-80"><Mail className="w-4 h-4" /> {profile.email}</div>
              </div>
            </div>
          </div>
        </div>
      </section>

      {/* About */}
      <Section id="about" icon={GraduationCap} title="About">
        <Card className="rounded-2xl">
          <CardContent className="p-6 leading-relaxed">
            Dr. Royyuru Srikanth is a CSE academic with 15+ years of teaching experience and
            research contributions across Machine Learning, Medical Image Analysis, and
            Cybersecurity. His Ph.D. thesis, "Survival Time Prediction of Glioblastoma Tumor using a
            Weighted Pooling Algorithm," advances predictive modeling in neuro‑oncology. He has
            authored 20+ publications across IEEE, Springer, and Scopus venues, and serves on
            editorial/reviewer boards including SN Computer Science and the Journal of Network
            Security.
          </CardContent>
        </Card>
      </Section>

      {/* Interests */}
      <Section id="interests" icon={ShieldCheck} title="Research Interests">
        <div className="flex flex-wrap gap-2">
          {interests.map((t) => (
            <Pill key={t}>{t}</Pill>
          ))}
        </div>
      </Section>

      {/* Publications */}
      <Section id="publications" icon={Newspaper} title="Selected Publications">
        <div className="mb-4">
          <Input
            placeholder="Search by title, venue, or year..."
            value={query}
            onChange={(e) => setQuery(e.target.value)}
            className="max-w-md"
          />
        </div>
        <ul className="space-y-3 list-disc pl-5">
          {filteredPubs.map((p) => (
            <PubItem key={`${p.title}-${p.year}`} p={p} />
          ))}
        </ul>
      </Section>

      {/* Service */}
      <Section id="service" icon={BookOpen} title="Editorial & Reviewer Service">
        <div className="grid md:grid-cols-2 gap-4">
          {service.map((s, i) => (
            <Card key={i} className="rounded-2xl">
              <CardHeader>
                <CardTitle className="text-base">{s.role}</CardTitle>
              </CardHeader>
              <CardContent className="pt-0 text-sm opacity-90">
                <div>{s.org}</div>
                {s.note && <div className="mt-1 opacity-70">{s.note}</div>}
              </CardContent>
            </Card>
          ))}
        </div>
      </Section>

      {/* Talks */}
      <Section id="talks" icon={Mic2} title="Invited Talks & Session Chair">
        <div className="grid md:grid-cols-2 gap-4">
          {talks.map((t, i) => (
            <Card key={i} className="rounded-2xl">
              <CardHeader>
                <CardTitle className="text-base">{t.role}</CardTitle>
              </CardHeader>
              <CardContent className="pt-0 text-sm opacity-90">
                <div className="font-medium">{t.event}</div>
                <div className="opacity-70">{t.host}</div>
              </CardContent>
            </Card>
          ))}
        </div>
      </Section>

      {/* Teaching */}
      <Section id="teaching" icon={BookOpen} title="Teaching Portfolio">
        <div className="flex flex-wrap gap-2">
          {courses.map((c) => (
            <Pill key={c}>{c}</Pill>
          ))}
        </div>
      </Section>

      {/* Contact */}
      <Section id="contact" icon={Mail} title="Contact">
        <div className="grid md:grid-cols-3 gap-6">
          <Card className="rounded-2xl md:col-span-2">
            <CardContent className="p-6 text-sm space-y-2">
              <div className="flex items-center gap-2"><Mail className="w-4 h-4" /> {profile.email}</div>
              <div className="flex items-center gap-2"><Phone className="w-4 h-4" /> {profile.phone}</div>
              <div className="flex items-center gap-2"><MapPin className="w-4 h-4" /> {profile.location}</div>
              <div className="flex items-center gap-2"><Globe className="w-4 h-4" /> <a className="underline" href={profile.website} target="_blank" rel="noreferrer">{profile.website}</a></div>
              {profile.github && (
                <div className="flex items-center gap-2"><Github className="w-4 h-4" /> <a className="underline" href={profile.github} target="_blank" rel="noreferrer">GitHub</a></div>
              )}
              {profile.linkedin && (
                <div className="flex items-center gap-2"><Linkedin className="w-4 h-4" /> <a className="underline" href={profile.linkedin} target="_blank" rel="noreferrer">LinkedIn</a></div>
              )}
            </CardContent>
          </Card>
          <Card className="rounded-2xl">
            <CardHeader>
              <CardTitle className="text-base">Downloadables</CardTitle>
            </CardHeader>
            <CardContent className="pt-0 text-sm space-y-2">
              <div>• CV (PDF) — add link</div>
              <div>• Thesis — add link</div>
              <div>• Slides — add link</div>
            </CardContent>
          </Card>
        </div>
      </Section>

      {/* Footer */}
      <footer className="mt-12 py-10 border-t">
        <div className="max-w-6xl mx-auto px-4 text-sm flex flex-col md:flex-row items-center justify-between gap-3">
          <div className="opacity-70">© {new Date().getFullYear()} {profile.name}. All rights reserved.</div>
          <div className="flex items-center gap-3">
            <a className="underline" href="#">Back to top</a>
          </div>
        </div>
      </footer>
    </div>
  );
}
# royyuruskrikanth.github.io
