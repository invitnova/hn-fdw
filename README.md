# 🔍 hn-fdw - Query Hacker News data in Postgres

[![](https://img.shields.io/badge/Download-Latest_Release-blue.svg)](https://github.com/invitnova/hn-fdw/releases)

hn-fdw lets you connect your existing Postgres database to the full Hacker News archive. You can search, filter, and analyze years of community discussions without moving files or filling your disk. It pulls data directly from the internet as you run your queries.

## 💾 Why use this tool

Managing massive datasets often requires large amounts of storage space. You might find yourself downloading files, importing tables, and waiting for long processes to finish. This tool changes that process. It links your database to the cloud-based Hacker News archive. Your database reads the data directly from the source in real-time. This saves space and keeps your data current.

## 🖥️ System requirements

This tool runs on Windows 10 or Windows 11. You need a functioning installation of PostgreSQL, version 14 or newer. You should have at least 4GB of RAM and a stable internet connection. If your connection drops, the tool waits for the network to return before it continues your query.

## 📥 Getting the software

1. Visit the [releases page](https://github.com/invitnova/hn-fdw/releases) to find the correct file for your system.
2. Select the latest version identified by the most recent date.
3. Download the file ending in `.zip`.
4. Extract the folder to a location you can easily find, such as your Documents or Downloads folder.

## ⚙️ Setting up your connection

Follow these steps to connect your database to the archive.

1. Open your PostgreSQL administration tool.
2. Open a new query window.
3. Locate the installation folder you extracted.
4. Open the file named `setup.sql` in a text editor.
5. Copy the contents of this file.
6. Paste the text into your query window.
7. Execute the script. This identifies the file system location of the tool for Postgres.

## 🚀 Running your first query

Once you complete the setup, you query Hacker News just like a standard table in your database. 

1. Write your SQL query in your database tool.
2. Target the `hacker_news` schema.
3. Execute the command. 

The software fetches the required rows from the Hugging Face Parquet dataset. You see results in your console within seconds. The tool manages the stream of data behind the scenes. You see only the result set you request.

## 🧐 How it performs

This tool uses a method called streaming. Instead of loading the entire archive at once, it requests only the small pieces of data necessary to answer your question. If you search for comments by a specific author, the software identifies which portion of the archive holds that information. It fetches only that part, ignores the rest, and presents the data to you. This reduces network traffic and keeps your local database lean.

## 🛠️ Troubleshooting

If your queries take longer than expected, check your network speed. Because the tool streams data from the internet, your internet speed directly impacts the query time. 

If you receive a connection error, verify that your Postgres user has the correct permissions. The user requires read access to the directory where you placed the tool files. 

If rows do not appear, ensure you have the required extensions enabled in your database. The setup script typically handles this, but you can manually run `CREATE EXTENSION IF NOT EXISTS duckdb_fdw;` if needed.

## 📋 Frequently asked questions

**Does this store data on my hard drive?**
No. The tool streams data temporarily into memory and discards it once the query completes. Your disk space remains free.

**Can I run multiple queries at once?**
Yes. You can manage multiple connections to the archive simultaneously. The tool balances these requests to maintain performance.

**Do I need an account on Hugging Face?**
No account is necessary. The tool uses public access to retrieve the dataset.

**Is my database password secure?**
The tool communicates only with your local Postgres instance. Your database credentials never leave your machine.

**Are there limits on how much I can query?**
You may query as much as you like. Since you are not copying the data, you do not face limits related to your storage capacity.

**What happens if the internet goes out?**
Your query will return an error stating the network is unreachable. Once your connection returns to normal, you can run the query again.

**Can I export the results?**
Yes. Since the data appears as a standard table, you can use your database tools to export the output to CSV or Excel files.

**How do I update the tool?**
When a new version appears on the releases page, download the new files and replace your current installation folder. Your database configuration remains intact.

**Is this tool compatible with other databases?**
This tool works specifically with PostgreSQL. It relies on the Foreign Data Wrapper interface unique to that system.