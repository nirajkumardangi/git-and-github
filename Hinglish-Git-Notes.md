# Git Master Class - Complete Notes in Hinglish 🚀

---

## 0:00 - Introduction

Git ek **Version Control System (VCS)** hai. Iska matlab hai ki ye tumhare code ki **har ek version/change ko track** karta hai.

**Socho aise:**
Tum ek essay likh rahe ho. Pehle draft likha, phir usme changes kiye, phir aur changes kiye. Agar tumhe kabhi purane draft pe jaana ho toh? Normally tum "essay_v1", "essay_v2", "essay_final", "essay_final_final" bana lete ho. Git ye sab **automatically** handle karta hai. Har change ka record rakhta hai, aur tum kabhi bhi kisi bhi purane version pe ja sakte ho.

**Git kyun zaroori hai?**

- Code ka **history** maintain hota hai
- **Multiple log** ek saath kaam kar sakte hain
- Galti ho jaaye toh **purane version pe wapas** ja sakte ho
- **Branching** se alag-alag features pe kaam kar sakte ho bina ek dusre ko disturb kiye

**Git vs GitHub/GitLab:**

- **Git** = Tool hai jo tumhare computer pe installed hota hai (local)
- **GitHub/GitLab** = Online platforms hain jahan tum apna Git repository upload (push) karte ho taaki doosre log bhi dekh sakein

---

## 1:03 - Verify Git Installation

Sabse pehle check karo ki Git tumhare system mein installed hai ya nahi.

**Command:**

```bash
git --version
```

Agar installed hai toh output aayega jaise:

```
git version 2.42.0
```

Agar nahi hai toh:

- **Windows:** [git-scm.com](https://git-scm.com) se download karo
- **Mac:** `brew install git`
- **Linux:** `sudo apt install git`

---

## 3:01 - Setting up Personal Info on Git (PREREQUISITE)

Jab bhi tum Git mein koi **commit** (change save) karte ho, toh Git ko ye jaanna hota hai ki **kisne** ye change kiya. Isliye apna naam aur email set karna zaroori hai.

**Commands:**

```bash
git config --global user.name "Tumhara Naam"
git config --global user.email "tumhara@email.com"
```

**`--global` ka matlab:**
Ye setting **poore system** ke liye apply hogi. Matlab har ek Git project mein ye naam aur email use hoga. Agar kisi specific project ke liye alag naam chahiye toh `--global` hata do.

**Check karne ke liye:**

```bash
git config --global user.name
git config --global user.email
```

Ya sabhi settings ek saath dekhne ke liye:

```bash
git config --list
```

**Theory behind this:**
Git ek **distributed** system hai. Har developer ka apna local copy hota hai. Jab multiple log kaam karte hain toh Git ko pata hona chahiye ki kaunsa change kisne kiya. Isliye ye identity setup zaroori hai. Ye information har commit ke saath permanently store hoti hai.

---

## 5:54 - Git Basic Commands | Study with Me

Yahan pe hum Git ke basic workflow samjhenge. Ye bahut important section hai.

### Git ka Basic Workflow - Teen Stages

Git mein koi bhi file **teen stages** se guzarti hai. Ye samajhna **bahut zaroori** hai:

```
Working Directory  →  Staging Area  →  Repository
   (git add)           (git commit)
```

**1. Working Directory (Workspace):**

- Ye wo folder hai jahan tum actually kaam kar rahe ho
- Jab tum koi file banate ho ya edit karte ho, wo changes yahan hote hain
- Git ko abhi tak in changes ke baare mein kuch nahi pata (untracked/modified)

**2. Staging Area (Index):**

- Ye ek **tayyari ka area** hai - ek middle zone
- Jab tum `git add` karte ho, toh file Working Directory se Staging Area mein aa jaati hai
- Iska matlab hai: "Haan, ye changes mujhe save karne hain"
- **Analogy:** Socho tum shopping kar rahe ho. Jo items tum **trolley** mein daalte ho, wo staging area hai. Abhi tak bill nahi hua (commit nahi hua), lekin tumne decide kar liya ki ye items chahiye.

**3. Repository (Local Repo / .git folder):**

- Jab tum `git commit` karte ho, staging area ka sara data **permanently save** ho jaata hai repository mein
- Ye tumhare project ka **history** ban jaata hai
- Har commit ek **snapshot** hoti hai - us waqt tumhare project ki poori photo
- **Analogy:** Trolley se items leke **billing counter** pe gaye aur payment kar diya. Ab ye final hai.

**Kyun 3 stages hain? Direct save kyun nahi?**
Socho tumne 10 files change ki. Lekin tum chahte ho ki sirf 3 files ka change save ho abhi. Toh tum sirf un 3 files ko staging area mein add karoge aur commit karoge. Baaki 7 files abhi working directory mein hi raheingi. Ye **granular control** deta hai.

### Important Basic Commands:

```bash
# Naya Git repository banana
git init

# Files ko staging area mein daalna
git add filename.txt        # Ek specific file
git add .                   # Saari files current directory ki

# Staged files ko permanently save karna
git commit -m "Yahan message likho ki kya change kiya"

# Current status dekhna (kaunsi file kahan hai)
git status

# History/log dekhna
git log
```

---

## 33:09 - Understanding git init

**`git init`** command se ek naye Git repository ki **shuruaat** hoti hai.

**Kya hota hai jab tum `git init` run karte ho?**

```bash
mkdir my-project
cd my-project
git init
```

Output:

```
Initialized empty Git repository in /path/my-project/.git/
```

Jab ye command chalti hai, toh tumhare folder ke andar ek **`.git`** naam ka hidden folder ban jaata hai. Ye `.git` folder hi **asli Git repository** hai. Iske andar Git apna sara data rakhta hai - commits, branches, config, sab kuch.

**`.git` folder ke andar kya hota hai?**

```
.git/
├── HEAD            → Current branch ka pointer
├── config          → Project-specific settings
├── objects/        → Saara data (commits, files, trees) yahan store hota hai
├── refs/           → Branches aur tags ke pointers
├── hooks/          → Automation scripts
└── ...aur bhi files
```

**Important Theory Points:**

1. **Ek folder mein ek hi baar `git init` karo.** Agar dobara karoge toh existing repository re-initialize ho jayegi (data usually nahi jaata, but avoid karo).

2. **`git init` sirf local repository banata hai.** Ye GitHub/GitLab se koi connection nahi banata. Wo baad mein `git remote add` se hota hai.

3. **Koi bhi folder ko Git repository bana sakte ho.** Empty folder ya phir already files wala folder, dono pe `git init` kaam karta hai.

4. **Nested git init se bachna chahiye.** Matlab ek git repo ke andar jaake dobara `git init` mat karo. Ye confusion create karta hai.

5. **Agar `.git` folder delete kar diya toh poora Git history gayab ho jayega.** Isliye `.git` folder ko kabhi mat chhedna manually (jab tak tum expert na ban jao).

---

## 43:02 - Understanding git status

**`git status`** command tumhe batata hai ki tumhare project ki **current situation** kya hai. Ye sabse zyada use hone wala command hai.

```bash
git status
```

**Ye command 4 cheezein batata hai:**

### 1. Untracked Files (Naye files)

```
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        newfile.txt
```

- Ye wo files hain jo tumne **nayi banayi** hain
- Git ne inhe kabhi track nahi kiya
- Ye **laal (red)** color mein dikhte hain
- Git keh raha hai: "Bhai ye file mujhe pata hi nahi hai, agar track karwana hai toh `git add` karo"

### 2. Modified Files (Purani files mein changes)

```
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
        modified:   oldfile.txt
```

- Ye wo files hain jo Git pehle se track kar raha tha, lekin tumne usme **kuch badla** hai
- Ye changes abhi **staging area mein nahi hain**
- Ye bhi **laal (red)** color mein dikhte hain

### 3. Staged Files (Commit ke liye ready)

```
Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        new file:   staged_file.txt
```

- Ye wo files hain jo tum `git add` karke **staging area** mein daal chuke ho
- Ye **hare (green)** color mein dikhte hain
- Ye next commit mein include hongi

### 4. Clean Working Tree

```
nothing to commit, working tree clean
```

- Matlab koi bhi pending change nahi hai
- Sab kuch commit ho chuka hai
- **Sab sorted hai!**

**File Lifecycle in Git:**

```
Untracked → Staged → Committed → Modified → Staged → Committed → ...
    ↑                                          ↑
  (new file)                              (edit existing)
```

**Theory: Git ke 4 File States:**

| State                    | Matlab                                            |
| ------------------------ | ------------------------------------------------- |
| **Untracked**            | Git ko is file ke baare mein pata nahi            |
| **Tracked - Unmodified** | Git track kar raha hai, koi change nahi hua       |
| **Tracked - Modified**   | Track ho rahi hai, change hua hai but staged nahi |
| **Tracked - Staged**     | Change staging area mein hai, commit ka wait      |

**Pro tip:** Har command se pehle aur baad mein `git status` run karo. Isse tumhe hamesha pata rahega ki kya ho raha hai.

---

## Advanced Git Commit: Deep Dive

`git commit` sirf code save karne ke liye nahi hai, balki yeh aapke project ki **history** aur **documentation** ka sabse bada pillar hai.

---

### 🏗 1. Conventional Commits (Industry Standard)
Professional teams ek fixed format use karti hain taaki automated tools (jaise semantic release) samajh sakein ki version number kab change karna hai.

**Format:** `<type>(<scope>): <description>`

| Type | Meaning | Example |
| :--- | :--- | :--- |
| **`feat`** | Naya feature add karna | `feat(auth): add JWT token validation` |
| **`fix`** | Koi bug fix karna | `fix(api): resolve null pointer in user-route` |
| **`refactor`** | Code cleanup (na bug fix, na feature) | `refactor: simplify database connection logic` |
| **`docs`** | Documentation mein change | `docs: update README with API endpoints` |
| **`style`** | Formatting (comma, semicolon, space) | `style: linting fixes in home component` |
| **`perf`** | Performance improve karne wala code | `perf: optimize image loading speed` |
| **`chore`** | Build tools ya dependencies update | `chore: upgrade tailwind to v4.0` |

---

### 🛠 2. Advanced Commit Clauses & Commands

**A. Modifying the Recent Past (`--amend`)**
Agar aapne commit kar diya par kuch bhool gaye (e.g., file add karna ya typo), toh naya commit banane ki zarurat nahi hai.
```bash
# Sirf message change karne ke liye
git commit --amend -m "Updated correct message"

# Bhooli hui file add karne ke liye
git add .
git commit --amend --no-edit
```
> **Rule:** Kabhi bhi wo commit `--amend` mat karo jo aap **Push** kar chuke ho. Isse remote history break ho sakti hai.

**B. Interactive Patch Commits (`-p`)**
Maano aapne `index.js` mein 50 lines likhi hain, par aap chahte ho ki 25 lines ek commit mein jayein aur baaki 25 dusre mein. 
```bash
git commit -p
```
Git aapko code ke **hunks** (tukde) dikhayega. Aap `y` (yes), `n` (no), ya `s` (split) daba kar chun sakte ho ki kitna code commit karna hai.



**C. Signing Commits (`-S`)**
Open source aur high-security projects mein commits ko GPG keys se sign kiya jata hai. Isse GitHub par "Verified" badge milta hai.
```bash
git commit -S -m "Secure and verified commit"
```

---

### 📝 3. Anatomy of a Great Commit Message
Bade changes ke liye hamesha **Multi-line Commit** ka use karein:

```bash
git commit
```
*(Editor khulne par niche diya gaya format likhein)*

```text
Summarize changes in around 50 characters (Subject Line)

More detailed explanatory text, if necessary. Wrap it to 
about 72 characters. Focus on:
- WHY this change was made.
- HOW it addresses the issue.
- Side effects or breaking changes.

Fixes #402 (Link to the issue)
```

---

### 💡 4. Expert Pro-Tips

**Atomic Commits**
Hamesha **"One Logical Change = One Commit"** ka rule follow karein. 
*   **Galat:** Ek hi commit mein "Navbar fix kiya, DB connect kiya, aur Typo sahi kiya".
*   **Sahi:** Teeno ke liye 3 alag-alag chote commits. Isse `git revert` karna asaan ho jata hai.

**Empty Commits**
Kabhi-kabhi aapko bina kisi code change ke commit karna padta hai (jaise CI/CD pipeline test karne ke liye).
```bash
git commit --allow-empty -m "Chore: trigger deployment pipeline"
```

**Verbose Mode**
Commit karte waqt agar aap dekhna chahte hain ki exactly kya changes ja rahe hain:
```bash
git commit -v
```
Yeh editor ke niche poora **diff** dikhayega taaki aap double-check kar sakein.

---

### 📊 Summary Table

| Feature | Command | Benefits |
| :--- | :--- | :--- |
| **Quick Fix** | `git commit --amend` | History clean rakhta hai. |
| **Partial Save** | `git commit -p` | Mixed code ko split karne ke liye. |
| **Shortcut** | `git commit -am` | Add aur commit ek saath (tracked files). |
| **Automation** | `feat/fix/...` | Professional changelogs generate karta hai. |

---

## 1:45:00 - Understanding git log (PREREQUISITE)

**`git log`** command tumhe tumhare project ka **poora history** dikhata hai - saare commits jo ab tak hue hain.

```bash
git log
```

**Output kuch aisa dikhta hai:**

```
commit a1b2c3d4e5f67890abcdef1234567890abcdef12 (HEAD -> main)
Author: Jatin <jatin@email.com>
Date:   Wed Dec 25 10:30:00 2024 +0530

    Add user authentication feature

commit 9x8y7z6w5v4u3t2s1r0qponmlkjihgfedcba98
Author: Jatin <jatin@email.com>
Date:   Tue Dec 24 15:00:00 2024 +0530

    Initial commit - project setup
```

### Har commit mein kya dikhta hai:

- **commit hash** - Unique ID (40 characters)
- **HEAD -> main** - Ye batata hai ki current branch kaunsi hai aur HEAD kahan point kar raha hai
- **Author** - Kisne commit kiya
- **Date** - Kab commit kiya
- **Message** - Kya kiya (commit message)

### HEAD kya hai?

**HEAD** ek **pointer** hai jo tumhare **current position** ko batata hai Git history mein.

**Analogy:** Socho ek kitaab hai aur usme **bookmark** lagaa hai. Tum jis page pe ho, wahan bookmark hai. HEAD wahi bookmark hai Git mein. Wo batata hai ki tum abhi kaunse commit pe khadhe ho.

Normally HEAD latest commit pe hota hai, lekin tum ise move bhi kar sakte ho purane commits pe (ye advanced topic hai).

### git log ke Different Variations:

```bash
# Simple one-line view (bahut useful)
git log --oneline
# Output:
# a1b2c3d (HEAD -> main) Add user authentication
# 9x8y7z6 Initial commit

# Graph view (branches visualize karne ke liye)
git log --oneline --graph
# Output:
# * a1b2c3d (HEAD -> main) Add authentication
# * 9x8y7z6 Initial commit

# Sirf last N commits dekhna
git log -3          # Last 3 commits
git log -5          # Last 5 commits

# Kisi particular file ka history
git log filename.txt

# Kisi author ke commits
git log --author="Jatin"

# Graph with all branches
git log --oneline --graph --all

# Detailed diff ke saath
git log -p
```

### Theory: Git log kyun important hai?

1. **Debugging:** Kab bug introduce hua, ye pata lagane ke liye
2. **Code Review:** Kisne kya change kiya ye dekhne ke liye
3. **Revert/Reset:** Kisi purane commit pe jaana ho toh uska hash chahiye
4. **Understanding:** Project ka evolution samajhne ke liye

---

## 2:00:33 - Undo Commits with git reset

**`git reset`** ka use hota hai **commits ko undo** karne ke liye. Ye tumhe **time travel** karne deta hai Git history mein - peeche ja sakte ho.

### git reset ke 3 Modes:

Ye samajhna **bahut important** hai. Teenon modes mein changes ko wapas karne ka tarika alag hai.

### 1. `git reset --soft <commit-hash>`

```bash
git reset --soft HEAD~1
```

**Kya hota hai:**

- Commit **undo** ho jaata hai
- Changes **staging area mein wapas aa jaate hain** (green)
- Working directory mein koi change nahi hota
- Basically sirf commit hata, baaki sab same

```
BEFORE: Working Dir → Staging → [Commit C] ← HEAD
AFTER:  Working Dir → [Staging has C's changes] → [Commit B] ← HEAD
```

**Analogy:** Tumne parcel pack karke courier counter pe de diya tha (commit). `--soft` ka matlab hai ki parcel counter se wapas le liya, lekin parcel abhi bhi packed hai (staging area mein hai). Sirf courier entry cancel hui.

**Kab use karein:** Jab commit message galat ho ya thoda aur change add karna bhool gaye ho.

### 2. `git reset --mixed <commit-hash>` (DEFAULT)

```bash
git reset HEAD~1
# ya
git reset --mixed HEAD~1
```

**Kya hota hai:**

- Commit **undo** ho jaata hai
- Changes **working directory mein wapas aa jaate hain** (red/untracked)
- Staging area **khaali** ho jaata hai
- Agar tum sirf `git reset` likho bina koi flag ke, toh **by default `--mixed`** hota hai

```
BEFORE: Working Dir → Staging → [Commit C] ← HEAD
AFTER:  [Working Dir has C's changes] → Empty Staging → [Commit B] ← HEAD
```

**Analogy:** Parcel courier counter se wapas le liya AUR parcel khol diya (unstaged). Ab items khule pade hain tumhare paas.

**Kab use karein:** Jab commit bhi undo karna ho aur decide karna ho ki kaunsi files dobara stage karni hain.

### 3. `git reset --hard <commit-hash>`

```bash
git reset --hard HEAD~1
```

**Kya hota hai:**

- Commit **undo** ho jaata hai
- Staging area **khaali** ho jaata hai
- Working directory bhi **us commit ki state pe chali jaati hai**
- **CHANGES PERMANENTLY DELETE HO JAATE HAIN!** ⚠️

```
BEFORE: Working Dir → Staging → [Commit C] ← HEAD
AFTER:  [Everything is like Commit B] → [Commit B] ← HEAD
```

**Analogy:** Parcel wapas le liya, khol diya, aur saara saamaan **kachre mein phek diya**. Ab kuch wapas nahi aayega.

**Kab use karein:** Jab tum pura yakeen ho ki wo changes chahiye hi nahi. **Bahut carefully use karo!**

### HEAD~1 ka matlab?

```
HEAD~1  → 1 commit peeche
HEAD~2  → 2 commits peeche
HEAD~3  → 3 commits peeche
```

Ya tum directly **commit hash** bhi de sakte ho:

```bash
git reset --soft a1b2c3d
```

### Summary Table:

| Mode      | Commit  | Staging Area           | Working Directory     |
| --------- | ------- | ---------------------- | --------------------- |
| `--soft`  | ❌ Undo | ✅ Changes rehte hain  | ✅ Changes rehte hain |
| `--mixed` | ❌ Undo | ❌ Khaali ho jaata hai | ✅ Changes rehte hain |
| `--hard`  | ❌ Undo | ❌ Khaali ho jaata hai | ❌ Changes DELETE     |

### ⚠️ Important Warning:

`git reset` **history change** karta hai. Agar tumne already commits push kar diye hain remote repository pe (GitHub), toh reset karna aur phir push karna **problematic** ho sakta hai team mein. Aise case mein `git revert` better hai.

---

## 2:11:36 - Undoing Commits with git revert

**`git revert`** bhi commits undo karta hai, lekin **safely**. Ye purana commit delete nahi karta, balki ek **nayi commit** banata hai jo purane changes ko **ulta** kar deti hai.

```bash
git revert <commit-hash>
```

### Reset vs Revert - Key Difference

**`git reset`** = History **mita deta** hai (commit gayab ho jaata hai)
**`git revert`** = History **add karta** hai (nayi commit aati hai jo purani ko cancel karti hai)

```
git reset scenario:
A → B → C (reset karke B pe gaye)
A → B ← HEAD  (C gayab!)

git revert scenario:
A → B → C (revert kiya C ko)
A → B → C → C' ← HEAD  (C' = C ke changes ka opposite)
```

### Analogy:

- **Reset** = Exam ka paper galat ho gaya, toh wo paper hi phad diya (history mita di)
- **Revert** = Exam ka paper galat ho gaya, toh ek nayi sheet pe likha "Q3 ka answer galat tha, sahi answer ye hai" (nayi entry add ki)

### Example:

Suppose tumne commit kiya "Added wrong config" aur uska hash hai `abc123`:

```bash
git revert abc123
```

Ye ek **nayi commit** create karega jismein `abc123` ke saare changes **ulte** ho jayenge. Purana commit history mein rahega (delete nahi hoga), lekin uske effects cancel ho jayenge.

### Kab Revert use karein vs Reset?

| Situation                              | Use             |
| -------------------------------------- | --------------- |
| Local commits (push nahi kiye)         | `git reset` ✅  |
| Already pushed commits (team ke saath) | `git revert` ✅ |
| History clean rakhna hai               | `git reset`     |
| Safe undo chahiye                      | `git revert`    |

### Theory:

`git revert` **safe** hai kyunki:

1. Koi history delete nahi hoti
2. Team mein koi conflict nahi aata
3. Kya undo hua, uska bhi **record** rehta hai
4. Agar revert galat ho gaya, toh revert ko bhi revert kar sakte ho!

---

## 2:23:04 - Understanding Branches in Git

Branches Git ka **sabse powerful feature** hai. Ye samajhna **bahut zaroori** hai.

### Branch kya hai?

Branch ek **alag line of development** hai. Socho ek road hai jis pe tum chal rahe ho (main branch). Ab ek mod aata hai aur ek nayi sadak banti hai (new branch). Dono sadkon pe alag-alag kaam ho sakta hai bina ek doosre ko disturb kiye.

### Kyun use karte hain Branches?

**Real-life scenario:**
Tum ek website bana rahe ho. Website live hai (main branch pe). Ab tumhe:

- Login feature add karna hai
- Payment system banana hai
- Bug fix karna hai

Agar teenon kaam seedha main branch pe karo toh:

- Code toot sakta hai
- Incomplete feature live ho sakta hai
- Sab gadbad ho jayega

**Solution: Branches!**

```
                    ← feature/login (alag branch)
main → A → B → C
                    ← feature/payment (alag branch)
                    ← bugfix/header (alag branch)
```

Har kaam ke liye alag branch banao, kaam complete karo, test karo, phir main branch mein merge karo.

### Default Branch:

- Jab tum `git init` karte ho, ek default branch banti hai
- Pehle ye **`master`** hoti thi, ab mostly **`main`** hoti hai
- Ye tumhari **production/stable** branch hai

### Branch Commands:

```bash
# Saari branches dekhna
git branch

# Nayi branch banana
git branch feature-login

# Branch switch karna (uspe jaana)
git checkout feature-login
# Ya (newer command)
git switch feature-login

# Nayi branch banana AUR uspe switch karna (2 kaam ek command mein)
git checkout -b feature-login
# Ya
git switch -c feature-login

# Branch delete karna
git branch -d feature-login

# Branch forcefully delete karna (unmerged branch)
git branch -D feature-login
```

### Branch internally kaise kaam karti hai?

Branch actually sirf ek **pointer** hai jo ek commit ko point karta hai. Jab tum nayi branch banate ho, toh ek naya pointer ban jaata hai jo **same commit** pe point karta hai jahan tum abhi ho.

```
main → C3
feature → C3   (abhi dono same jagah hain)
HEAD → feature  (tum feature branch pe ho)
```

Jab tum feature branch pe nayi commit karte ho:

```
main → C3
feature → C4 (aage badh gaya)
HEAD → feature
```

Main branch abhi bhi C3 pe hai, feature C4 pe aa gaya. **Dono independent hain.**

### HEAD aur Branch ka relation:

**HEAD** hamesha **current branch** ko point karta hai. Jab tum branch switch karte ho, HEAD us branch pe move ho jaata hai.

```bash
# HEAD → main
git switch feature
# HEAD → feature
git switch main
# HEAD → main
```

### Practical Example:

```bash
# Main branch pe ho
git branch          # * main

# Nayi branch banao
git branch feature-login

# Switch karo
git switch feature-login

# Kaam karo
echo "login code" > login.js
git add .
git commit -m "Add login feature"

# Main pe wapas jao
git switch main
# Yahan login.js nahi dikhega! Kyunki wo feature branch pe hai

# Feature branch pe jao
git switch feature-login
# login.js wapas aa gaya!
```

**Ye jaadu hai branches ka** - har branch ka apna alag state hota hai.

---

## 2:50:12 - Understanding Revisiting Branch

Ye section branches ko **aur deeply** samajhne ke baare mein hai.

### Branch Pointer Movement:

```
Initial State:
main: A → B → C ← HEAD

Create feature branch:
main: A → B → C ← HEAD
feature:        ↑ (same commit C pe point kar rahi hai)

Switch to feature and make commit:
main: A → B → C
                 ↘
feature:          D ← HEAD

Make another commit on feature:
main: A → B → C
                 ↘
feature:          D → E ← HEAD

Switch back to main and make commit:
main: A → B → C → F ← HEAD
                 ↘
feature:          D → E
```

Ab main aur feature **diverge** ho gayi hain - dono alag directions mein gaye.

### Important Concepts:

1. **Branch create karna free hai** - koi extra space nahi lagta (sirf pointer hai)
2. **Branch switch karne pe files change hoti hain** - working directory us branch ke hisaab se update ho jaati hai
3. **Uncommitted changes le jaana** - Agar tumne changes commit nahi kiye aur branch switch karo, toh Git ya toh changes saath le jayega ya error dega (conflict hone pe)

### Detached HEAD State:

```bash
git checkout <commit-hash>
```

Agar tum directly kisi purane **commit pe switch** karte ho (branch pe nahi), toh tum **"detached HEAD"** state mein aa jaate ho. Matlab HEAD kisi branch ko point nahi kar raha, seedha commit ko point kar raha hai.

Isme kiye gaye commits **lost** ho sakte hain agar tum wapas branch pe switch karo bina nayi branch banaye.

---

## 3:24:01 - Understanding Git Merging

**Merging** ka matlab hai do branches ke kaam ko **ek saath milana** (combine karna).

### Merging kyun?

Tumne feature branch pe kaam kiya, testing ho gayi, sab sahi hai. Ab ye changes main branch mein laane hain. Ye process hai **merging**.

### Merge kaise karte hain?

**Rule:** Tum jis branch MEIN merge karna chahte ho, **pehle us branch pe jaao**, phir merge command do.

```bash
# Main branch pe jaao
git switch main

# Feature branch ko main mein merge karo
git merge feature-login
```

### Merge ke Types (Scenarios):

### Scenario 1: Fast-Forward Merge

```
BEFORE:
main: A → B → C
                 ↘
feature:          D → E

(main pe C ke baad koi nayi commit nahi hai)

AFTER merge:
main: A → B → C → D → E ← HEAD
```

**Kya hua?** Main branch ka pointer seedha aage move ho gaya feature ke latest commit pe. Koi nayi merge commit nahi bani. Ye **sabse simple** merge hai.

**Kab hota hai?** Jab main branch pe feature branch banne ke baad koi nayi commit nahi aayi ho. Main seedha aage badh sakta hai.

**Analogy:** Tum ek line mein khadhe ho. Tumhare aage koi nahi hai. Toh tum seedha aage badh jaate ho. Koi conflict nahi.

---

## 3:37:51 - Git Merging Scenario 2 Important

### Scenario 2: Three-Way Merge (Recursive Merge)

```
BEFORE:
main: A → B → C → F → G
                 ↘
feature:          D → E

(main pe bhi nayi commits aayi hain - F, G)

AFTER merge:
main: A → B → C → F → G → M (merge commit) ← HEAD
                 ↘         ↗
feature:          D → E
```

**Kya hua?** Dono branches pe changes hue hain (main pe F,G aur feature pe D,E). Git dono ke changes ko combine karta hai aur ek **nayi merge commit (M)** banata hai. Is merge commit ke **2 parents** hote hain - main ka last commit aur feature ka last commit.

**Kab hota hai?** Jab dono branches pe alag-alag commits ho gayi hain aur dono diverge ho gayi hain.

**Three-Way kyun kehte hain?** Git teen cheezein compare karta hai:

1. **Common ancestor** (C - jahan se dono branches alag hue)
2. **Main branch ka latest** (G)
3. **Feature branch ka latest** (E)

In teenon ko compare karke Git samajhta hai ki kya merge karna hai.

**Analogy:** Do log ek hi document ki copy leke alag-alag changes karte hain. Ab dono ke changes ek document mein merge karne hain. Isliye original document (ancestor) se compare karna padta hai ki kisne kya badla.

---

## 3:51:45 - Git Merge Scenario Implementation

Practical implementation:

```bash
# Step 1: Main branch pe initial commits
git switch main
echo "Hello World" > index.html
git add .
git commit -m "Initial commit"

# Step 2: Feature branch banao
git switch -c feature-navbar

# Step 3: Feature branch pe kaam karo
echo "<nav>Navbar</nav>" > navbar.html
git add .
git commit -m "Add navbar"

# Step 4: Main pe wapas jao aur kuch kaam karo
git switch main
echo "<footer>Footer</footer>" > footer.html
git add .
git commit -m "Add footer"

# Step 5: Feature branch ko main mein merge karo
git switch main
git merge feature-navbar
# Ye three-way merge hoga kyunki dono branches pe commits hain
# Ek merge commit banega
```

---

## 4:02:34 - Understanding How to Resolve Merge Conflict in Branches

### Merge Conflict kya hai?

Jab **dono branches mein same file ki same line** ko differently edit kiya gaya ho, toh Git confuse ho jaata hai - "Main kiska change rakhun?" Ye situation hai **merge conflict**.

```
main branch:   line 5 → "Hello World"
feature branch: line 5 → "Hello Git"
```

Git sochta hai: "Dono ne line 5 change ki hai, mujhe kaise pata kaunsa sahi hai?"

Isliye Git merge **rok deta** hai aur tumse kehta hai: "Bhai, ye tum khud decide karo."

### Conflict kaise dikhta hai?

Jab conflict hota hai, Git conflicted file mein **markers** daal deta hai:

```
<<<<<<< HEAD
Hello World
=======
Hello Git
>>>>>>> feature-branch
```

**Explanation:**

- `<<<<<<< HEAD` se `=======` tak → **Current branch (main)** ka code
- `=======` se `>>>>>>> feature-branch` tak → **Incoming branch (feature)** ka code

### Conflict kaise resolve karein?

**Step 1:** File kholo aur decide karo kya rakhna hai:

```
# Option A: Main ka rakhna hai
Hello World

# Option B: Feature ka rakhna hai
Hello Git

# Option C: Dono ka rakhna hai
Hello World
Hello Git

# Option D: Kuch naya likhna hai
Hello Everyone
```

**Step 2:** Saare conflict markers (`<<<<<<<`, `=======`, `>>>>>>>`) hatao

**Step 3:** File save karo

**Step 4:** Stage aur commit karo

```bash
git add .
git commit -m "Resolve merge conflict in index.html"
```

### Theory: Conflict kyun hota hai?

- Jab **same file ki same lines** dono branches mein change ho
- Jab ek branch mein file **delete** hui aur doosri mein **edit** hui
- Git sirf un changes ko automatically merge kar sakta hai jo **alag-alag files ya alag-alag lines** mein hue hain

### Conflict se kaise bachein?

1. **Choti branches banao** - Jitna kam time branch alag rahegi, utna kam conflict chance
2. **Regularly main se pull karo** - Feature branch mein main ke changes lete raho
3. **Communication** - Team mein baat karo kaun kaunsi file pe kaam kar raha hai
4. **Chhoti chhoti commits karo** - Resolve karna aasan hoga

---

## 4:17:17 - Picking Just Particular Commits with git cherry-pick

**`git cherry-pick`** ek bahut interesting command hai. Isse tum kisi **doosri branch se sirf ek specific commit** utha ke apni current branch mein laga sakte ho.

### Normal Merge vs Cherry-pick:

- **Merge:** Poori branch ke saare commits le aata hai
- **Cherry-pick:** Sirf ek (ya kuch specific) commits le aata hai

### Command:

```bash
git cherry-pick <commit-hash>
```

### Example:

```
main: A → B → C ← HEAD
feature: A → B → D → E → F
```

Tumhe sirf commit **E** chahiye main branch mein (D aur F nahi chahiye):

```bash
git switch main
git cherry-pick <E-ka-hash>
```

Result:

```
main: A → B → C → E' ← HEAD
```

**E'** ek nayi commit hai jismein E ke same changes hain but different hash (kyunki parent alag hai).

### Analogy:

Socho ek basket mein bahut saare fruits hain (commits). Tum poori basket nahi chahte (merge), sirf ek apple uthana chahte ho (cherry-pick). 🍒

### Kab use karein?

- Kisi doosri branch se sirf ek specific bug fix chahiye
- Feature branch se sirf particular feature ka commit chahiye
- Galti se wrong branch pe commit kar diya, toh sahi branch pe cherry-pick karo

---

## 4:19:01 - Git Revision Part 1 - Study with Me

Ye ek revision section hai jahan pe ab tak ke saare concepts revise kiye jaate hain:

### Quick Recap:

```
1. git init          → Naya repo start
2. git status        → Current situation
3. git add           → Staging area mein daalo
4. git commit        → Permanently save karo
5. git log           → History dekho
6. git reset         → Commits undo (history change)
   --soft            → Changes staging mein
   --mixed           → Changes working dir mein (default)
   --hard            → Changes delete (DANGEROUS!)
7. git revert        → Safe undo (nayi commit banake)
8. git branch        → Branches manage karo
9. git switch/checkout → Branch switch karo
10. git merge        → Branches combine karo
11. git cherry-pick  → Specific commit uthao
```

### Workflow Diagram:

```
Working Directory
      ↓ git add
Staging Area (Index)
      ↓ git commit
Local Repository (.git)
      ↓ git push (baad mein padhenge)
Remote Repository (GitHub/GitLab)
```

---

## 5:12:28 - Understanding Remote Repository

Ab tak jo kuch bhi kiya wo sab **local** tha - tumhare computer pe. Ab hum **remote repository** ke baare mein samjhenge.

### Remote Repository kya hai?

Remote repository ek **server pe hosted** copy hai tumhare Git project ki. Ye internet pe hoti hai taaki:

1. **Backup** - Computer crash ho jaaye toh bhi code safe hai
2. **Collaboration** - Team ke log access kar sakein
3. **Sharing** - Doosron ko code dikha sako

### Popular Remote Hosting Platforms:

| Platform      | URL           |
| ------------- | ------------- |
| **GitHub**    | github.com    |
| **GitLab**    | gitlab.com    |
| **Bitbucket** | bitbucket.org |

### Local vs Remote:

```
Tumhara Computer (Local)          Internet (Remote)
┌──────────────────┐              ┌──────────────────┐
│  Working Dir     │              │                  │
│  Staging Area    │  ──push──→   │  Remote Repo     │
│  Local Repo      │  ←──pull──   │  (GitHub/GitLab) │
│  (.git folder)   │              │                  │
└──────────────────┘              └──────────────────┘
```

### Theory: Distributed Version Control

Git **distributed** hai, matlab:

- Har developer ke paas **complete copy** hoti hai repository ki (poora history)
- Remote server pe bhi complete copy hoti hai
- Koi bhi developer offline kaam kar sakta hai
- Internet mile toh remote se sync kar lo

Ye **centralized** systems (like SVN) se alag hai jahan sirf server pe poora code hota tha.

---

## 5:19:40 - Creating Account in GitLab

GitLab ek platform hai jahan tum apne remote repositories host kar sakte ho.

**Steps:**

1. [gitlab.com](https://gitlab.com) pe jao
2. Sign up karo (email, username, password)
3. Account verify karo
4. Dashboard pe aake nayi repository bana sakte ho

(GitHub pe bhi same process hai - [github.com](https://github.com) pe jao aur sign up karo)

---

## 5:20:01 - Understanding git remote add and git push

### git remote add

Ye command tumhare local repository ko **remote repository se connect** karta hai.

```bash
git remote add origin https://gitlab.com/username/project-name.git
```

**Breakdown:**

- `git remote add` → Remote connection add karo
- `origin` → Remote ka naam (convention hai "origin" rakhna, but kuch bhi rakh sakte ho)
- `URL` → Remote repository ka address (GitLab/GitHub se milta hai)

**`origin` kya hai?**

- Ye sirf ek **nickname** hai remote URL ke liye
- Baar baar poora URL type karne ke bajaye, sirf "origin" likhna padta hai
- Tum multiple remotes bhi add kar sakte ho alag naam se

```bash
# Remote connections dekhna
git remote -v

# Output:
# origin  https://gitlab.com/username/project.git (fetch)
# origin  https://gitlab.com/username/project.git (push)
```

### git push

Ye command tumhare **local commits ko remote repository pe bhejta** hai.

```bash
git push origin main
```

**Breakdown:**

- `git push` → Bhejo
- `origin` → Kahan bhejne hai (remote ka naam)
- `main` → Kaunsi branch bhejni hai

**Pehli baar push karte waqt:**

```bash
git push -u origin main
```

`-u` (ya `--set-upstream`) ka matlab hai ki **tracking relationship set karo**. Iske baad aage se sirf `git push` likhna kaafi hai, branch aur remote ka naam dobara nahi likhna padega.

### Push ka flow:

```
Local Repo → (git push) → Remote Repo
Commits jo local pe hain but remote pe nahi → Remote pe pahunch jaate hain
```

### Theory Points:

1. Push **sirf committed changes** bhejta hai (staging area ya working directory ke changes nahi)
2. Agar remote pe koi aur pehle push kar chuka hai, tumhe pehle **pull** karna padega (baad mein padhenge)
3. Push ke liye **authentication** chahiye (username/password ya SSH key)

---

## 5:45:55 - Revisiting git log for a moment!

Remote ke baad `git log` mein kuch naye cheezein dikhti hain:

```bash
git log --oneline
```

```
a1b2c3d (HEAD -> main, origin/main) Add feature
9x8y7z6 Initial commit
```

**Naye terms:**

- **HEAD -> main** → Tum local main branch pe ho
- **origin/main** → Remote (origin) ki main branch bhi isi commit pe hai

Agar tumne local pe commit kiya lekin push nahi kiya:

```
b3c4d5e (HEAD -> main) New local commit
a1b2c3d (origin/main) Add feature
```

Dekho - `HEAD -> main` aage hai aur `origin/main` peeche hai. Matlab local pe ek commit zyada hai jo remote pe abhi nahi gayi.

```bash
git push  # Iske baad dono same ho jayenge
```

---

## 5:49:51 - Understanding git clone

**`git clone`** command se tum kisi **remote repository ki poori copy** apne computer pe download kar sakte ho.

```bash
git clone https://gitlab.com/username/project-name.git
```

### Kya hota hai jab clone karte ho?

1. Ek **naya folder** ban jaata hai project ke naam se
2. Usme **saari files** aa jaati hain
3. **Poora Git history** aa jaata hai (saari branches, saare commits)
4. **Remote connection** (origin) **automatically set** ho jaata hai
5. Default branch pe **checkout** ho jaata hai

### Clone vs Init:

| `git init`                          | `git clone`                                  |
| ----------------------------------- | -------------------------------------------- |
| **Naya** empty repo banata hai      | **Existing** repo ki copy banata hai         |
| Koi file nahi aati                  | Saari files + history aati hai               |
| Remote manually set karna padta hai | Remote automatically set hota hai            |
| Tum project start kar rahe ho       | Tum kisi aur ke project mein join ho rahe ho |

### Analogy:

- `git init` = Nayi diary kharidi, khali hai, ab likhna shuru karo
- `git clone` = Kisi ki diary ki **photocopy** le li, saare pages aa gaye

### Custom folder name ke saath clone:

```bash
git clone https://gitlab.com/username/project-name.git my-folder-name
```

---

## 5:59:04 - Understanding git pull and git fetch

Ye dono commands **remote se local mein changes laate hain**, lekin dono mein **fundamental difference** hai.

### Overall Concept:

```
Remote Repo (GitHub/GitLab)
     ↓
git fetch → Sirf download karta hai, merge nahi karta
git pull  → Download + Merge dono karta hai
```

**Key Formula:**

```
git pull = git fetch + git merge
```

---

## 6:13:31 - Understanding git fetch

**`git fetch`** remote repository se latest changes **download** karta hai, lekin tumhare working code mein **koi change nahi** karta.

```bash
git fetch origin
# Ya simply
git fetch
```

### Kya hota hai fetch mein?

1. Remote pe jo nayi commits hain, wo **download** ho jaati hain
2. `origin/main` pointer **update** ho jaata hai
3. Tumhari local `main` branch **same rehti hai** (koi change nahi)
4. Tumhara working directory **safe** hai

```
BEFORE fetch:
Remote:  A → B → C → D → E
Local:   A → B → C (origin/main bhi yahan)

AFTER fetch:
Remote:  A → B → C → D → E
Local:   A → B → C ← main (HEAD)
                  ↓
         origin/main → E  (pointer update ho gaya)
```

### Ab changes dekhne ke liye:

```bash
# Kya aaya hai remote se
git log origin/main

# Local vs Remote difference
git diff main origin/main
```

### Merge karna ho toh manually karo:

```bash
git merge origin/main
```

### Analogy:

**Fetch** = Amazon se parcel aaya, **delivery boy ne building ke neeche rakh diya** (downloaded). Tumhare ghar mein (working directory) abhi kuch nahi aaya. Tum chaaho toh neeche jaake le aao (merge karo), chaaho toh mat lo.

### Kab use karein?

- Jab dekhna ho ki remote pe kya naya aaya hai **bina apna code disturb kiye**
- Team mein kaam kar rahe ho aur pehle review karna chahte ho ki kya changes aaye hain
- **Safe** approach chahiye

---

## 6:27:21 - Understanding git pull

**`git pull`** remote se changes **download + merge** dono ek saath karta hai.

```bash
git pull origin main
# Ya simply
git pull
```

### Kya hota hai pull mein?

1. Remote se latest changes **download** hote hain (fetch)
2. Wo changes **automatically merge** ho jaate hain tumhari current branch mein
3. Tumhara working directory **update** ho jaata hai

```
BEFORE pull:
Remote:  A → B → C → D → E
Local:   A → B → C ← main (HEAD)

AFTER pull:
Remote:  A → B → C → D → E
Local:   A → B → C → D → E ← main (HEAD)
```

### Analogy:

**Pull** = Amazon se parcel aaya aur **seedha tumhare ghar mein deliver** ho gaya. Ab tumhare paas hai.

### Fetch vs Pull - Comparison:

| Feature             | `git fetch`   | `git pull`                          |
| ------------------- | ------------- | ----------------------------------- |
| Download changes    | ✅            | ✅                                  |
| Auto merge          | ❌            | ✅                                  |
| Working dir changes | ❌            | ✅                                  |
| Safe?               | Zyada safe    | Thoda risky (conflict aa sakta hai) |
| Control             | Zyada control | Kam control                         |
| Kab use?            | Review first  | Jaldi chahiye                       |

### ⚠️ Pull mein conflict aa sakta hai!

Agar tumne local pe bhi changes kiye hain aur remote pe bhi kisi ne same file edit ki hai, toh pull karte waqt **merge conflict** aa sakta hai. Use same tarike se resolve karna padega jaise branch merge mein karte hain.

### Best Practice:

```bash
# Pehle fetch karo
git fetch

# Dekho kya aaya
git log --oneline origin/main

# Sab theek lage toh merge karo
git merge origin/main

# Ya seedha pull karo agar trust hai
git pull
```

---

## 6:33:36 - Store changes temporarily using git stash

**`git stash`** tumhare **uncommitted changes ko temporarily save** kar deta hai bina commit kiye. Jaise kisi safe mein rakh diya.

### Problem jo stash solve karta hai:

Tum feature branch pe kaam kar rahe ho, aadha kaam hua hai (commit karne layak nahi hai). Tabhi boss bolta hai "main branch pe ek urgent bug fix karo!"

Ab problem ye hai ki:

- Tum branch switch nahi kar sakte kyunki changes uncommitted hain
- Commit nahi karna chahte kyunki kaam aadha hai
- Changes delete bhi nahi karna chahte

**Solution: `git stash`!**

### Commands:

```bash
# Changes stash karo (temporarily save)
git stash
# Ya message ke saath
git stash save "work in progress on login"

# Stash list dekho
git stash list
# Output:
# stash@{0}: WIP on feature: abc123 work in progress on login
# stash@{1}: WIP on feature: def456 some other stash

# Stash wapas laao (aur stash se hatao)
git stash pop

# Stash wapas laao (lekin stash mein bhi rakho)
git stash apply

# Specific stash apply karo
git stash apply stash@{1}

# Stash delete karo
git stash drop stash@{0}

# Saare stash delete karo
git stash clear
```

### Stash ka Flow:

```
1. Working Directory mein changes hain (uncommitted)
2. git stash → Changes TEMPORARILY hat gaye, directory clean ho gayi
3. Branch switch karo, bug fix karo, commit karo
4. Wapas aao original branch pe
5. git stash pop → Changes WAPAS aa gaye!
```

### Analogy:

Tum kitchen mein khana bana rahe ho (feature development). Doorbell bajti hai (urgent kaam). Tum **saara saamaan fridge mein rakh dete ho** (stash). Door pe jaake kaam karte ho. Wapas aake **fridge se saamaan nikaalte ho** (stash pop) aur khana banana continue karte ho.

### Theory Points:

1. Stash ek **stack** data structure follow karta hai (LIFO - Last In First Out)
2. Multiple stash kar sakte ho
3. Stash **branch-independent** hai - ek branch pe stash kiya, doosri pe pop kar sakte ho
4. **Tracked files** by default stash hoti hain. Untracked files ke liye `-u` flag lagao:
   ```bash
   git stash -u
   ```

---

## 6:40:15 - Ignore Files using .gitignore

### Problem:

Har project mein kuch files hoti hain jo tumhe Git mein track **nahi karni** chahiye:

- `node_modules/` (bahut bada folder, npm install se wapas aa jaata hai)
- `.env` (passwords, API keys - sensitive information)
- Log files (`.log`)
- OS files (`.DS_Store` on Mac, `Thumbs.db` on Windows)
- Build folders (`dist/`, `build/`)
- IDE settings (`.vscode/`, `.idea/`)

Ye files agar Git mein aa gayi toh:

- Repository ka size bahut badh jayega
- Sensitive data leak ho sakta hai
- Unnecessary changes track honge

### .gitignore file kya hai?

Ye ek special file hai jismein tum likhte ho ki **kaunsi files/folders Git ko ignore karni hain**.

### Kaise banaye?

Project ke **root folder** mein ek file banao naam `.gitignore`:

```bash
touch .gitignore
```

### .gitignore mein kya likhein?

```gitignore
# Ye ek comment hai

# Specific file ignore
secret.txt
.env

# Specific folder ignore (/ lagao end mein)
node_modules/
dist/
build/

# Particular extension ki saari files ignore
*.log
*.tmp
*.cache

# Pattern matching
*.pyc
__pycache__/

# Exception - ye file TRACK karo (! se negate)
!important.log

# Nested folder mein file ignore
logs/debug.log

# Saare folders mein koi bhi .env file ignore
**/.env
```

### Important Rules:

1. **`.gitignore` file khud commit honi chahiye** - taaki team ke sabhi log same files ignore karein
2. **Already tracked files ignore nahi hongi** - Agar pehle se koi file track ho rahi hai, toh `.gitignore` mein daalne se wo ignore nahi hogi. Pehle untrack karo:

   ```bash
   git rm --cached filename.txt
   ```

   `--cached` ka matlab sirf Git se hatao, file system se mat delete karo.

3. **Global gitignore** bhi bana sakte ho:
   ```bash
   git config --global core.excludesfile ~/.gitignore_global
   ```

### Theory: Kyun zaroori hai?

| Ignore karo     | Reason                                          |
| --------------- | ----------------------------------------------- |
| `node_modules/` | Bahut bada, `npm install` se wapas aata hai     |
| `.env`          | Passwords, API keys - **security risk!**        |
| `*.log`         | Temporary files, har machine pe alag            |
| `.DS_Store`     | OS-specific, har machine pe alag                |
| `build/`        | Generated files, source se wapas ban sakte hain |

---

## 🎯 COMPLETE SUMMARY - Ek nazar mein poora Git

```
LOCAL COMMANDS:
├── git init            → Naya repo start
├── git status          → Current situation dekho
├── git add             → Staging area mein daalo
├── git commit          → Permanently save karo
├── git log             → History dekho
├── git reset           → Commits undo (dangerous)
│   ├── --soft          → Changes staging mein
│   ├── --mixed         → Changes working dir mein
│   └── --hard          → Changes DELETE!
├── git revert          → Safe undo (nayi commit)
├── git branch          → Branches manage karo
├── git switch          → Branch switch karo
├── git merge           → Branches combine karo
├── git cherry-pick     → Specific commit uthao
├── git stash           → Temporarily changes save karo
└── .gitignore          → Files ignore karo

REMOTE COMMANDS:
├── git remote add      → Remote connection jodo
├── git push            → Local → Remote bhejo
├── git clone           → Remote → Local copy lo
├── git fetch           → Download (merge nahi)
└── git pull            → Download + Merge (fetch + merge)
```

### Complete Workflow:

```
1. git init / git clone
2. Files create/edit karo
3. git add .
4. git commit -m "message"
5. git push origin main
6. (Doosre log) git pull
7. Repeat 2-6
```
