# Free Windows Cloud PC — GitHub se (Sirf Free Resources)

Ye project GitHub Actions ke free Windows runner ko 6 ghante ke liye
Remote Desktop PC bana deta hai. Koi credit card nahi, koi paid service nahi.

**Free cheezein jo use hongi:**
- GitHub account (free) — Public repo par Actions minutes unlimited hote hain standard runners ke liye
- Tailscale (free personal plan) — RECOMMENDED, secure connection, card nahi mangta
- YA ngrok (free account) — Alternative tariqa
- Microsoft Remote Desktop app (free) — Mobile / PC se connect karne ke liye

**Specs jo milengi:** Windows Server runner, ~4 vCPU, ~16 GB RAM (public repo), ~14 GB disk
**Limit:** Ek session max 6 ghante, phir PC band ho jata hai aur data delete ho jata hai.
Dobara Run karne par naya fresh PC milta hai. Ye permanent PC nahi hai.

---

## Method 1 — Tailscale (Asan aur Secure, Recommended)

### Step 1: Naya GitHub Repo banao
1. github.com par login karo > New repository
2. Name: `free-windows-pc` — **Public** select karo (free unlimited minutes ke liye)
3. Is project ki files us repo me upload karo (`.github` folder समेत)

### Step 2: Tailscale Free Account + Auth Key
1. tailscale.com par Google/GitHub se free signup karo
2. Apne mobile/PC par bhi Tailscale app install karke same account se login karo
3. tailscale.com/admin/settings/keys par jao > Generate auth key
   - Reusable: ON kar do (taake har dafa nayi key na banani pare)
4. Key copy kar lo (tskey-auth-... se start hogi)

### Step 3: GitHub Repo me Secrets add karo
Repo > Settings > Secrets and variables > Actions > New repository secret

| Secret Name | Value |
|---|---|
| `TAILSCALE_AUTH_KEY` | Step 2 wali key |
| `RDP_PASSWORD` | Apna strong password, maslan `MeraPC@2026!` (yehi login password hoga) |

### Step 4: PC Start karo
Repo > Actions tab > **Free Windows PC - Tailscale** > Run workflow

2-3 minute wait karo. Jab log me `AAP KA WINDOWS PC READY HAI` aur
`Tailscale IP: 100.x.x.x` aye, PC ready hai.

### Step 5: Connect karo
- **Windows PC se:** Remote Desktop Connection app kholo > IP daalo > Username: `runneradmin` > Password: jo secret me rakha tha
- **Android/iPhone se:** Microsoft Remote Desktop / Windows App kholo > + > PC name me wohi IP daalo
- Note: Tumhare apne device par Tailscale ON aur same account login hona lazmi hai, warna connect nahi hoga.

### Band karna
Actions tab > chal raha workflow > Cancel workflow. Warna 6 ghante baad khud band ho jayega.

---

## Method 2 — ngrok (Agar Tailscale na use karna ho)

1. ngrok.com par free signup > dashboard.ngrok.com/get-started/your-authtoken se token lo
2. Repo Secrets me add karo:
   - `NGROK_AUTH_TOKEN` = woh token
   - `RDP_PASSWORD` = apna password
3. Actions > **Free Windows PC - ngrok** > Run workflow
4. Log me `Address: 0.tcp.ngrok.io:xxxxx` milega — wohi Remote Desktop me daalna hai.
   Is method me Tailscale ki zaroorat nahi, lekin address public hota hai, is liye strong password lazmi rakho.

---

## Zaruri Warnings

1. **Data save nahi rehta** — Zaroori files Google Drive / OneDrive par rakho, PC par nahi.
2. **GitHub ki policy:** Actions ko sirf remote PC ke tor par lagatar use karna GitHub ki Terms ke khilaf ja sakta hai aur account restrict ho sakta hai. Ise occasional / testing / seekhne ke liye use karo, 24/7 server mat banao. Apna main GitHub account risk par hai to alag account par test karo.
3. **Password kabhi share mat karo**, aur workflow log / ngrok address bhi kisi ko mat bhejo — jo bhi us address + password jane ga woh PC me ghus sakta hai.
4. **Public repo** me kabhi password ya key code me mat likho — hamesha Secrets me rakho, jaise is project me hai.

## Dobara Chalana
Har dafa Actions > Run workflow. Har dafa naya PC, nayi Tailscale IP milegi
(Tailscale admin panel me purani offline machines delete kar sakte ho).
