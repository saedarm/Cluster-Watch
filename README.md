```markdown
# Finance Forecast – Insider Cluster Buys + Zacks Rankings

Automated Node.js + React app that:  

- Scrapes **OpenInsider** for cluster buys > $250,000.  
- Queries **Zacks API** for Buy/Hold/Sell rankings of tickers with insider activity.  
- Stores results in **MongoDB Atlas**.  
- Sends a **daily email** summary with top insider activity and Zacks ranking.  
- Displays the results on a **React frontend** with manual refresh option.  
- Fully setup and run with **one command** — no Docker required.  

---

## 🔗 Project URLs

- **OpenInsider:** [https://openinsider.com](https://openinsider.com)  
- **Zacks API npm:** [https://www.npmjs.com/package/zacks-api](https://www.npmjs.com/package/zacks-api)  
- **MongoDB Atlas:** [https://www.mongodb.com/cloud/atlas](https://www.mongodb.com/cloud/atlas)  

---

## 🗂️ Project Structure

```

finance-forecast/
├── backend/
│   ├── server.js
│   ├── models/stockData.js
│   ├── routes/stockRoutes.js
│   ├── services/zacksService.js
│   ├── services/emailService.js
│   ├── utils/scheduler.js
│   ├── .env
│   ├── package.json
│   └── package-lock.json
├── frontend/
│   ├── src/
│   │   ├── App.js
│   │   ├── components/StockList.js
│   │   ├── components/StockChart.js
│   │   ├── pages/Dashboard.js
│   │   └── index.js
│   ├── public/index.html
│   ├── package.json
│   └── package-lock.json
├── tasks.js
├── .gitignore
└── README.md

````

---

## ⚙️ Prerequisites

- Node.js >= 18  
- npm >= 9  
- MongoDB Atlas account  
- Gmail account (for daily email, using **App Password**)  

---

## 📝 One-Command Setup

### 1. Clone the repository

```bash
git clone <your-github-repo-url>
cd finance-forecast
````

### 2. Run everything with one command

```bash
npm run start-all
```

What happens:

1. Creates `backend/.env` if missing (you will need to edit it with real credentials).
2. Installs `backend` and `frontend` dependencies.
3. Launches **backend** (`http://localhost:5000`) and **frontend** (`http://localhost:3000`) concurrently.
4. Scheduler in backend fetches **OpenInsider + Zacks** daily and emails top stocks to `searmentrout@gmail.com`.

---

## 📝 Backend `.env`

After running `npm run start-all`, edit `backend/.env`:

```dotenv
MONGO_URI=mongodb+srv://<username>:<password>@<cluster>.mongodb.net/finance
EMAIL_USER=your_email@gmail.com
EMAIL_PASS=your_gmail_app_password
PORT=5000
```

> Replace `<username>`, `<password>`, `<cluster>` with your MongoDB Atlas credentials.
> Use a Gmail **App Password** for `EMAIL_PASS`.

---

## 📊 Backend API Endpoints

| Endpoint             | Method | Description                                            |
| -------------------- | ------ | ------------------------------------------------------ |
| `/api/stocks`        | GET    | Fetch latest Zacks + insider data (auto-updated daily) |
| `/api/stocks/stored` | GET    | Get all stored stock data from MongoDB                 |

---

## 🖥️ Frontend

* Dashboard displays **insider cluster buys + Zacks rankings**.
* Refresh button can manually trigger backend fetch (optional).
* Runs on: `http://localhost:3000`

---

## 📧 Daily Email

* Sent daily at **8 AM ET** automatically via `node-cron`.
* Shows **top 10 stocks** with insider buys > $250k and Zacks rank + rating.

Example table:

| Ticker | Company | Total Insider Buy ($) | Insiders                 | Zacks Rank | Rating |
| ------ | ------- | --------------------- | ------------------------ | ---------- | ------ |
| TSLA   | Tesla   | 450,000               | Elon Musk, Zach Kirkhorn | 2          | Buy    |
| AAPL   | Apple   | 300,000               | Tim Cook                 | 3          | Hold   |

---

## 🔄 Manual Refresh

* Frontend button can trigger `/api/stocks` to fetch **instant Zacks + insider data**.
* Useful for updates outside the 8 AM daily schedule.

---

## ⚡ Notes

* `fetchClusterBuys()` scrapes **OpenInsider** for **cluster buys > $250,000**.
* `fetchZacksData()` queries **Zacks API** only for tickers returned from OpenInsider.
* All data stored in MongoDB daily is displayed in frontend and sent via email.
* Cron schedule is configurable in `backend/utils/scheduler.js`.

---

## 🔧 Developer Workflow

```bash
git clone <repo-url>
cd finance-forecast
npm run start-all   # sets up everything and starts backend + frontend
```

* Backend: `http://localhost:5000`
* Frontend: `http://localhost:3000`
* Daily email sent to `searmentrout@gmail.com`

> One command sets everything up and starts the full stack. No Docker required.

---

## 🔗 Acknowledgments

* **Zacks API Integration**: This project leverages the [zacks-api](https://github.com/janlukasschroeder/zacks-api) library by [Jan Lukas Schroeder](https://github.com/janlukasschroeder) to retrieve Zacks investment research data.
```
