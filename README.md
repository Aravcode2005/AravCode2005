rror: 'portfolio/' does not have a commit checked out
error: unable to index file 'portfolio/'
fatal: adding files failed
[autisticbaboon@stars Portfolio-Traveller]$

Bro, this happens because your portfolio/ folder contains its own .git directory, so Git treats it as a nested repository (potential submodule) instead of a normal folder.
Fix: Make portfolio/ part of your main repository

From your Portfolio-Traveller directory, run:

1. Check for nested Git:

ls -la portfolio/

Look for .git.

2. Remove the nested Git metadata:

rm -rf portfolio/.git

This removes the Git history/configuration inside portfolio/, not your actual project files. Only do this if you don't need that separate repository history.

3. Add and commit your files:

git add .
git commit -m "Add portfolio website"

Why this happened

Your folder structure probably looks like:
Portfolio-Traveller/
├── .git/            ← Main Git repository
└── portfolio/
    ├── .git/        ← Nested Git repository (problem)
    ├── src/
    ├── package.json
    └── ...

Git is trying to add portfolio/ as a repository reference rather than its contents.

If portfolio/ is supposed to be a standalone Git repository or submodule, don't delete its .git; it needs a different setup.

For your portfolio project, if you want everything in one GitHub repository, removing the nested .git is usually the right fix.
utisticbaboon@stars Portfolio-Traveller]$ git add .
warning: adding embedded git repository: portfolio/Portfolio
hint: You've added another git repository inside your current repository.
hint: Clones of the outer repository will not contain the contents of
hint: the embedded repository and will not know how to obtain it.
hint: If you meant to add a submodule, use:
hint:
hint:   git submodule add <url> portfolio/Portfolio
hint:
hint: If you added this path by mistake, you can remove it from the
hint: index with:
hint:
hint:   git rm --cached portfolio/Portfolio
hint:
hint: See "git help submodule" for more information.
hint: Disable this message with "git config set advice.addEmbeddedRepo false"
[autisticbaboon@stars Portfolio-Traveller]$
…

Bro 😭 you've got another nested Git repository!

Your folder structure is probably:
Portfolio-Traveller/
├── .git/                  ← Main repository
└── portfolio/
    └── Portfolio/
        ├── .git/          ← Another Git repository
        ├── src/
        └── package.json

Git is warning you that portfolio/Portfolio will be tracked as an embedded repository, not as ordinary project files.
Fix it without losing your project files

From Portfolio-Traveller, first check:

ls -la portfolio/Portfolio/

If you want everything inside one GitHub repository, and don't need the inner repository's separate Git history, run:

1. Unstage the embedded repository

git rm --cached -r portfolio/Portfolio

2. Remove its nested Git metadata

rm -rf portfolio/Portfolio/.git

This deletes the inner repository's Git history and configuration, not your website source code. Make sure you don't need that history first.

3. Add everything again

git add .
git status

4. Commit

git commit -m "Add portfolio project"

Important

If you discover more nested repositories, check them with:

find . -name .git -print

For a single-repository setup, you generally want only:
./.git

The key idea: One main Git repository should manage your portfolio files. Any nested .git directories need to be intentionally configured as submodules or removed if you want their files tracked normally.
[autisticbaboon@stars Portfolio-Traveller]$ git rm --cached -r portfolio/Portfolio
error: the following file has staged content different from both the
file and the HEAD:
    portfolio/Portfolio
(use -f to force removal)
[autisticbaboon@stars Portfolio-Traveller]$

Git is refusing because portfolio/Portfolio has staged changes.

Since you want to track the actual portfolio files rather than a nested repository, use -f with --cached.
1. Force remove it from Git's staging area

git rm -r -f --cached portfolio/Portfolio

This does not delete your project files. It only removes the embedded repository entry from Git's index.
2. Remove the nested .git directory

First verify it:

ls -la portfolio/Portfolio/.git

If you don't need the inner repository's separate Git history:

rm -rf portfolio/Portfolio/.git

3. Add your files again

git add .
git status

You should now see individual files such as:
new file: portfolio/Portfolio/package.json
new file: portfolio/Portfolio/src/App.jsx

Instead of:
new file: portfolio/Portfolio
4. Commit

git commit -m "Add portfolio website"

Important: git rm --cached is safe for your working files, but deleting the nested .git permanently removes that repository's local history and configuration.

If another nested-repository warning appears, run:

find . -name .git -print

and share the output before deleting anything else.

<!--
  ARAV GUPTA / GitHub profile README
  Theme: dark terminal + signal green
  Place this file in: github.com/Aravcode2005/Aravcode2005
-->

<div align="center">

<img width="100%" src="https://capsule-render.vercel.app/api?type=waving&height=235&color=0:060911,45:102638,100:00dba5&text=ARAV%20GUPTA&fontColor=f3fff9&fontSize=63&fontAlignY=42&desc=SYSTEMS%20%2F%20SECURITY%20%2F%20INFRASTRUCTURE&descSize=17&descAlignY=64&animation=fadeIn" alt="Arav Gupta — Systems, Security and Infrastructure" />

<a href="https://git.io/typing-svg"><img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=500&size=17&pause=1200&color=00DBA5&center=true&vCenter=true&width=750&height=45&lines=I+build+systems.+Then+I+trace+how+they+fail.;Linux+%E2%86%92+Containers+%E2%86%92+Cloud+%E2%86%92+Security;Shipping+code+is+the+start%2C+not+the+finish." alt="Animated introduction" /></a>

Backend & Infrastructure Engineer in the making
B.Tech CSE (AI/ML) @ VIT Bhopal · 2024–2028 · New Delhi, India

<a href="https://github.com/Aravcode2005"><img src="https://img.shields.io/badge/GitHub-121923?style=for-the-badge&logo=github&logoColor=00DBA5" alt="GitHub" /></a>
<a href="https://www.linkedin.com/in/arav-gupta/"><img src="https://img.shields.io/badge/LinkedIn-121923?style=for-the-badge&logo=linkedin&logoColor=00DBA5" alt="LinkedIn" /></a>
<a href="https://leetcode.com/u/Aravg2005/"><img src="https://img.shields.io/badge/LeetCode-121923?style=for-the-badge&logo=leetcode&logoColor=00DBA5" alt="LeetCode" /></a>
<a href="mailto:aravlead@gmail.com"><img src="https://img.shields.io/badge/Email-121923?style=for-the-badge&logo=gmail&logoColor=00DBA5" alt="Email" /></a>
</div>

00 / whoami
arav@linux:~$ cat /proc/about-me

role       : backend + infrastructure builder
focus      : application security, Linux, cloud, DevSecOps
approach   : understand the failure, not just the fix
currently  : building, breaking assumptions, documenting what I learn
I work across the boundaries where software tends to get interesting: application logic, authentication, container networking, CI/CD, cloud permissions, and the operating system underneath it all.

I'm especially interested in security engineering grounded in systems knowledge — access controls that are enforced, trust boundaries that are explicit, and recovery plans that actually work.
01 / proof-of-work
<table>
<tr>
<td width="50%" valign="top">

<strong>🔐 <a href="https://github.com/Aravcode2005/HireFlow">HireFlow / AirHire</a></strong>

<em>Recruitment automation · Node.js · AWS</em>
<ul>
<li>Implemented administrator onboarding with <strong>JWT/session authentication</strong>, expiring OTPs, and attempt controls.</li>
<li>Built scheduled <strong>Playwright</strong> workflows and integrations with Gmail and Google Calendar APIs.</li>
<li>Containerized application components and built a <strong>Jenkins → Amazon ECR</strong> delivery pipeline.</li>
</ul>
<code>App security</code> · <code>Auth</code> · <code>CI/CD</code>

</td>
<td width="50%" valign="top">


<strong>🎮 <a href="https://github.com/Aravcode2005/pixelManiac">PixelMania</a></strong>

<em>Real-time 3D multiplayer · Node.js · Socket.IO</em>
<ul>
<li>Built a <strong>30 Hz server-authoritative simulation</strong>: clients send input intent; the server owns movement, collisions, damage, and match state.</li>
<li>Isolated multiplayer room state; used <strong>MongoDB</strong> for persistence and <strong>Redis</strong> for ephemeral session data.</li>
<li>Built containerized deployment and versioned <strong>Jenkins → ECR → EC2</strong> delivery.</li>
</ul>
<code>Trust boundaries</code> · <code>Distributed state</code> · <code>AWS</code>

</td>
</tr>
</table>

02 / the-incident-log
My favorite debugging stories happen below the framework.

Encrypted Linux recovery — Arch Linux · LUKS · SHA-256 · S3
- Installed Arch Linux with a LUKS-encrypted root filesystem and worked through an encrypted-root boot failure after partition changes.
- Recovered access using a verified LUKS header backup.
- Archived MongoDB and MySQL data, plus Docker volumes, to Amazon S3 and validated archive integrity using cryptographic hashes.
Cloud and container troubleshooting — AWS · Docker · Jenkins
- Investigated AWS security-group connectivity and IAM permission denials.
- Debugged Jenkins DNS failures, Docker socket/group access, container networking, and reverse-proxy upstream resolution.
- Worked with Docker Compose, Redis health checks, Nginx, and Caddy while deploying multi-service applications.
These are hands-on engineering and recovery experiences — not claims of formal penetration testing or security audits.
03 / toolbox
Layer	Tools and concepts
Security & identity	LUKS, JWT, OTP controls, SHA-256 integrity checks, Linux permissions, AWS IAM/security-group troubleshooting
Operating systems	Arch Linux, Ubuntu, Amazon Linux, Bash, process and network debugging
Cloud & delivery	AWS EC2, ECR, S3, Elastic Beanstalk, Docker, Docker Compose, Jenkins, Git
Backend & data	Node.js, Express, REST APIs, Socket.IO, MongoDB, Redis, MySQL, PostgreSQL
Programming	JavaScript, TypeScript, Python, C++, Java, Go


04 / field-experience
When	What	Where
Apr – Jul 2026	Business Development Intern & Software Project Contributor; built HireFlow/AirHire	JP IT Staffing
May – Jul 2026	AI Intern / DT FDE Fellow; product features and research	DeepThought CultureTech Ventures
Jan 2026 – Present	Technical research contributor; environmental sensing and filtration study	Delhi Air Quality Research Initiative


Additional signals: 460+ DSA problems · SOLVIT 2025 finalist · VIT × JHU Health Hackathon finalist · GSSoC & SSoC 2026 contributor
05 / currently-exploring
[+] Linux security internals and recovery workflows
[+] AWS identity, authorization and network boundaries
[+] Safer container and CI/CD architectures
[+] Observability, incident analysis and distributed systems
<div align="center">

06 / telemetry
<img height="160" src="https://github-readme-stats.vercel.app/api?username=Aravcode2005&show_icons=true&hide_border=true&bg_color=060911&title_color=00dba5&text_color=b6c8c6&icon_color=00dba5" alt="GitHub activity statistics" />
<img height="160" src="https://github-readme-stats.vercel.app/api/top-langs/?username=Aravcode2005&layout=compact&hide_border=true&bg_color=060911&title_color=00dba5&text_color=b6c8c6" alt="Most used GitHub languages" />

Good infrastructure doesn't just deploy. It explains itself when it breaks.

<a href="mailto:aravlead@gmail.com">Let's talk about systems, infrastructure, or security engineering.</a>
<img width="100%" src="https://capsule-render.vercel.app/api?type=waving&height=110&section=footer&color=0:00dba5,55:102638,100:060911" alt="Footer wave" />

</div>
make my github readme free like my soul and also add  this portfolio link ,it should look soooooooooooooooooooooooooooooooooooo nicceeeeeeeeeeeee
…
Worked for 1m 7s

BROOOOO. 🌌 This time, I wanted your GitHub to feel like a little universe of your own, not another engineering résumé.

I created a complete GitHub profile README for you.

ARAV GUPTA — Somewhere Between the Terminal and the Stars
Aurora Over Majestic Alpine Peaks - backiee

The atmosphere behind the new design: dark, spacious, adventurous, with subtle emerald-green terminal accents.
What I changed

    More personality: “A builder, a learner, a wanderer.” Your profile now reflects the human behind the terminal.

    Cinematic introduction: Animated typing text, dark colors, and a clean visual identity.

    Your portfolio is featured prominently: traveller-smoky.vercel.app appears near the top, within your projects, and at the end.

    Engineering credibility stays: HireFlow, PixelMania, Linux recovery, infrastructure troubleshooting, and your actual technical experience.

    A more personal ending: Less corporate language, more curiosity, creativity, and independence.

Your new GitHub README

199 lines · Markdown + GitHub-compatible HTML

 Download README.md
How to put it on your GitHub

Open your special profile repository:

github.com/Aravcode2005/Aravcode2005

Replace the contents of its README.md with this file and commit the change. GitHub will automatically display it on your profile.

One line from the new README that captures the direction:

    There's more to life than uptime, commits, and green checkmarks.

I deliberately kept the engineering sections substantial. The goal isn't to hide your technical work behind aesthetics—it's to show that the person building those systems has an entire life beyond them.
README.mdDocument
<div align="center"><img width="100%" src="https://capsule-render.vercel.app/api?type=waving&height=245&color=0:080d19,45:123c48,100:15d8b0&text=ARAV%20GUPTA&fontColor=effffb&fontSize=63&fontAlignY=40&desc=BUILD%20%E2%80%A2%20BREAK%20%E2%80%A2%20UNDERSTAND%20%E2%80%A2%20REBUILD&descSize=16&descAlignY=62&animation=fadeIn" alt="Arav Gupta header" />
<a href="https://readme-typing-svg.demolab.com/demo/"> <img src="https://readme-typing-svg.demolab.com?font=JetBrains+Mono&weight=500&size=17&duration=3200&pause=950&color=37E2BE&center=true&vCenter=true&width=780&height=54&lines=Somewhere+between+the+terminal+and+the+stars.;I+build+systems.+Then+I+learn+how+they+fail.;Curious+mind.+Restless+soul.+Open+road.;Still+learning.+Still+building.+Still+becoming." alt="Typing introduction" /> </a>

Engineering systems. Exploring everything else.

Linux · Backend · Cloud · Security · DevSecOps

B.Tech CSE (AI/ML) · VIT Bhopal · 2024–2028

<a href="https://traveller-smoky.vercel.app/"><img src="https://img.shields.io/badge/EXPLORE_MY_WORLD-15D8B0?style=for-the-badge&logo=vercel&logoColor=071017&labelColor=15D8B0" alt="Explore my portfolio" /></a>
<a href="https://github.com/Aravcode2005"><img src="https://img.shields.io/badge/GITHUB-111827?style=for-the-badge&logo=github&logoColor=ffffff" alt="GitHub" /></a>
<a href="https://www.linkedin.com/in/arav-gupta/"><img src="https://img.shields.io/badge/LINKEDIN-111827?style=for-the-badge&logo=linkedin&logoColor=37E2BE" alt="LinkedIn" /></a>
<a href="https://leetcode.com/u/Aravg2005/"><img src="https://img.shields.io/badge/LEETCODE-111827?style=for-the-badge&logo=leetcode&logoColor=37E2BE" alt="LeetCode" /></a>
<a href="mailto:aravlead@gmail.com"><img src="https://img.shields.io/badge/SAY_HELLO-111827?style=for-the-badge&logo=gmail&logoColor=37E2BE" alt="Email" /></a>



“Not everything that matters fits inside a commit.”
</div>
01 / the human behind the terminal
arav@stars:~$ whoami

  a builder, a learner, a wanderer.
  fascinated by what happens beneath the interface.
  drawn to quiet places, difficult problems, and open skies.

arav@stars:~$ cat /etc/interests

  systems engineering   ████████████████
  security & cloud      ███████████████░
  creative experiments  ██████████████░░
  exploring the world   ████████████████

I love the space where software meets reality: when a container cannot reach its service, an IAM policy behaves differently than expected, or a machine refuses to boot. I want to know why, not just which command makes the error disappear.

I build backend systems and infrastructure, explore security through hands-on engineering, and make creative things outside the terminal too. There is no single box I particularly want to stay in.

    My rule: Keep the curiosity. Question the assumptions. Build things that survive contact with the real world.

02 / things I've brought to life
<table> <tr> <td width="50%" valign="top">

🔐
HireFlow / AirHire

<sub>Recruitment automation · Node.js · AWS</sub>



    Administrator onboarding with JWT/session authentication, expiring OTPs, and attempt controls.
    Scheduled Playwright workflows with Gmail and Google Calendar integrations.
    Containerized services and a Jenkins → Amazon ECR delivery pipeline.

Authentication Automation CI/CD
</td> <td width="50%" valign="top">

🎮
PixelMania

<sub>Real-time 3D multiplayer · Socket.IO</sub>



    30 Hz server-authoritative simulation for movement, collisions, damage, and match state.
    Isolated multiplayer rooms; MongoDB persistence and Redis session data.
    Containerized Jenkins → ECR → EC2 deployments.

Real-time systems State AWS
</td> </tr> <tr> <td width="50%" valign="top">

🌍 My digital home

<sub>Personal portfolio · art, experiments, engineering</sub>



A home for the things I make and the parts of myself that don't fit neatly into a résumé.

Step inside →

Portfolio Creativity The journey
</td> <td width="50%" valign="top">

🧭 The next frontier

<sub>Systems security · cloud infrastructure</sub>



Exploring deterministic security checks, infrastructure trust boundaries, and safer ways to ship software.

Some ideas are still diagrams. Some are experiments. That's part of building.

DevSecOps Linux Learning in public
</td> </tr> </table>
03 / stories from the trenches

🔓 Bringing an encrypted Linux machine back to life
Installed Arch Linux with a LUKS-encrypted root filesystem, worked through a boot failure after partition changes, and recovered access using a verified LUKS header backup. Archived database data and Docker volumes to S3 and checked integrity with cryptographic hashes.

☁️ Following failures through the stack
Debugged AWS security-group connectivity and IAM denials; Jenkins DNS and Docker permissions; container networking, health checks, and reverse-proxy resolution. Worked across Docker Compose, Redis, Nginx, and Caddy.

<sub>Hands-on engineering and recovery experience — not a claim of formal penetration-testing or audit work.</sub>
04 / the toolkit
<div align="center"><img src="https://skillicons.dev/icons?i=linux,bash,aws,docker,jenkins,git,github,nginx,nodejs,express,redis,mongodb,mysql,postgres,js,ts,python,cpp,java,go&perline=10" alt="Technology icons" /></div>
Layer	What I work with
Systems	Arch Linux, Ubuntu, Amazon Linux, Bash, process/network debugging
Cloud & delivery	AWS EC2, ECR, S3, Elastic Beanstalk, Docker, Jenkins, Git
Backend & data	Node.js, Express, REST, Socket.IO, MongoDB, Redis, MySQL, PostgreSQL
Security	LUKS, JWT, OTP controls, SHA-256, IAM, network boundaries
Languages	JavaScript, TypeScript, Python, C++, Java, Go
05 / footprints along the way

    JP IT Staffing — Business Development Intern & Software Project Contributor · Apr–Jul 2026
    DeepThought CultureTech Ventures — AI Intern / DT FDE Fellow · May–Jul 2026
    Delhi Air Quality Research Initiative — Technical research contributor · Jan 2026–present

460+ DSA problems · SOLVIT 2025 finalist · VIT × JHU Health Hackathon finalist · GSSoC & SSoC 2026 contributor
06 / live signals
<div align="center"><img height="165" src="https://github-readme-stats.vercel.app/api?username=Aravcode2005&show_icons=true&hide_border=true&bg_color=080d19&title_color=37e2be&text_color=c2d7d7&icon_color=37e2be" alt="GitHub statistics" /> <img height="165" src="https://github-readme-stats.vercel.app/api/top-langs/?username=Aravcode2005&layout=compact&hide_border=true&bg_color=080d19&title_color=37e2be&text_color=c2d7d7" alt="GitHub language statistics" />
<img src="https://komarev.com/ghpvc/?username=Aravcode2005&style=flat-square&color=15d8b0&label=visitors+passing+through" alt="Profile views" /></div><div align="center">
07 / beyond the code

There's more to life than uptime, commits, and green checkmarks.

I like the road with no particular destination, the night sky, learning something just because it looks impossible, and making things simply because they feel worth making.

If you came here for the code, I hope you found something useful.
If you came here for the person, this is the longer story.

Stay curious. Stay a little untamed.

<a href="https://traveller-smoky.vercel.app/"><img src="https://img.shields.io/badge/↗_ENTER_THE_PORTFOLIO-15D8B0?style=for-the-badge&labelColor=0B1720&color=15D8B0" alt="Open portfolio" /></a>
<img width="100%" src="https://capsule-render.vercel.app/api?type=waving&height=125&section=footer&color=0:15d8b0,50:123c48,100:080d19" alt="Footer wave" /></div>


