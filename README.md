# 📊 Elasticsearch-Filebeat-Kibana Stack for Nginx Log Monitoring

Welcome! This project helps you monitor and visualize your web server's activity in real-time. Think of it as a security camera 📹 for your web server that records everything and shows you what happened!

## 🎯 What Is This Project?

Imagine you own a restaurant 🍕 and want to know:
- How many customers came today? ✅
- What time was it busiest? ✅
- Did anything go wrong? ⚠️

This project does the same thing for your **Nginx web server**! It automatically:
1. **Records** everything your web server does
2. **Collects** those records in one place
3. **Shows you** nice visualizations and charts

## 📚 Simple Explanation of Each Component

### 🌐 **Nginx** (Your Web Server)
This is like a waiter at the restaurant 🤵. It takes customer requests and serves them what they want. Every action it takes (like "Customer ordered coffee ☕") gets written down in logs.

### 📝 **Filebeat** (The Secretary)
This is like a secretary 📋 who walks around reading everything the waiter writes down and sends it to the manager's office. It reads log files and sends the information forward.

### 🔍 **Elasticsearch** (The Big Storage & Search Engine)
Think of this as a **huge library with a superpower** 📚✨. Instead of just storing information like a regular library, it can search through millions of records instantly! You ask it "Show me all failures from today" and it finds them in milliseconds.

### 📊 **Kibana** (The Dashboard)
This is like a **smart TV showing you statistics** 📺. It takes information from Elasticsearch and shows you beautiful charts and graphs. You can see trends, patterns, and problems at a glance.

---

## 🗂️ Project Structure (What Files Do What)

```
NGINX-EFK/
│
├── 📁 nginx/                    # Your web server folder
│   ├── Dockerfile             # Instructions to build nginx
│   ├── nginx.conf             # Settings for nginx
│   └── 📁 logs/               # Folder where logs are saved
│       ├── access.log         # "Customer visited page X at Y time"
│       └── error.log          # "Oops! Something went wrong!"
│
├── 📁 filebeat/               # The secretary's folder
│   └── filebeat.yml           # Instructions for filebeat
│
├── docker-compose.yml         # Master control file (starts everything)
└── README.md                  # This file!
```

---

## 🔄 How Everything Works Together

Let's trace a customer's journey 👇

```
1️⃣ Customer visits your website
         ↓
2️⃣ Nginx records: "Customer from IP visited /page.html at 3:45 PM - Success! ✅"
         ↓
3️⃣ Nginx writes this to access.log file
         ↓
4️⃣ Filebeat reads the new line: "Hey, there's something new!"
         ↓
5️⃣ Filebeat sends it to Elasticsearch: "Store this information"
         ↓
6️⃣ Elasticsearch saves it in its database like a library 📚
         ↓
7️⃣ You open Kibana and see a nice chart showing "100 visitors today!" 📊
```

**In simple words**: Log file → Filebeat → Elasticsearch → Kibana Dashboard ✅

---

## ✅ What You Need Before Starting

You need to install these two things on your computer:

### 🐳 **Docker**
Think of Docker as a magic box 📦. Instead of installing software normally (which can be messy), you just put everything in a box and it works the same everywhere!

```bash
# Check if Docker is installed
docker --version
```

### 🐋 **Docker Compose**
This is like a **remote control** 🎮 for Docker. Instead of starting each box one by one, you press one button and all boxes start together!

```bash
# Check if Docker Compose is installed
docker-compose --version
```

**Don't have them?** 
- [Install Docker](https://www.docker.com/products/docker-desktop)
---

## 🚀 How To Start (Step By Step)

### Step 1️⃣: Get Ready
Open your terminal/command prompt and navigate to your project folder:

```bash
cd your-project-directory
```

### Step 2️⃣: Start Everything
Run this one magical command:

```bash
docker-compose up -d
```

**What does `-d` mean?** It means "start in the background" so you can still use your terminal.

The computer will now:
- ✅ Build the Nginx box
- ✅ Download Elasticsearch, Kibana, and Filebeat boxes
- ✅ Start all boxes at the same time
- ✅ Connect them together

### Step 3️⃣: Check If Everything Started
```bash
docker-compose ps
```

You should see something like:
```
NAME              STATUS
nginx             Up 2 minutes ✅
elasticsearch     Up 2 minutes ✅
kibana            Up 2 minutes ✅
filebeat          Up 2 minutes ✅
```

All showing ✅ means success!

### Step 4️⃣: Wait a Bit (Important!)
Elasticsearch is like a car engine 🚗 - it needs time to warm up. Wait **30-60 seconds**, then check if it's ready:

```bash
curl http://localhost:9200
```

If you see information about Elasticsearch version, you're good to go! ✅

---

## 🎮 How To Use It

### 🌐 Visit Your Website
Open your web browser and go to:
```
http://localhost
```

You should see: **"Hello from Nginx!"** 👋

### 📊 Open Kibana Dashboard
This is where the magic happens! Open:
```
http://localhost:5601
```

You'll see a beautiful dashboard! 🎨

### 🔍 View Your Logs

**First time users - Follow these steps:**

1. In Kibana, click on **Menu** (☰ icon) at the top left
2. Go to **Stack Management** → **Data Views**
3. Click **Create Data View**
4. For the name, type: `filebeat-*` (this tells Kibana where to find the logs)
5. For timestamp field, select: `@timestamp`
6. Click **Save Data View**

**Now view your logs:**
1. Click on **Menu** (☰ icon) again
2. Click on **Discover**
3. Make sure `filebeat-*` is selected in the dropdown
4. You'll see all the logs! 📝
5. Each line shows what happened:
   - **Who** visited (IP address)
   - **When** they visited (time)
   - **What** they requested (page/file)
   - **Did it work?** (success ✅ or error ❌)

### 🛑 Stop Everything
When you're done, run:

```bash
docker-compose down
```

This stops all containers. Your logs are saved! ✅

To delete everything (including stored data):

```bash
docker-compose down -v
```

⚠️ This deletes all your logs and database! Use only if you want to start fresh.

---
