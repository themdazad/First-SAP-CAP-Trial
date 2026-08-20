# SAP CAP Application
Simple starter project using **SAP CAP**, **Node.js**, and **SQLite**.

---

## Getting Started

Welcome to the CAP project.<br>
The project follows the basic CAP structure:

| Folder | Purpose |
|---|---|
| `app/` | UI applications and frontend-related files |
| `db/` | Database models, schema, and mock data |
| `srv/` | Service definitions and business logic |

### Start the Project

Open the terminal inside the project and run:

```bash
cds watch
```

In VS Code, you can also use:

**Terminal → Run Task → cds watch**

The application will normally be available at:

```text
http://localhost:4004
```

---

## Setup SAP CAP CLI

### npm EACCES Error on macOS

If you run:

```bash
npm i -g @sap/cds-dk
```

and get:

```text
EACCES: permission denied, mkdir '/usr/local/lib/node_modules/@sap'
```

npm does not have permission to write to the global system directory.

Instead of using `sudo`, use a user-owned npm directory.

### Fix

Create a global npm directory:

```bash
mkdir -p ~/.npm-global
```

Tell npm to use it:

```bash
npm config set prefix ~/.npm-global
```

Add it to PATH:

```bash
echo 'export PATH="$HOME/.npm-global/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc
```

Now install CAP:

```bash
npm init -y
npm i -g @sap/cds-dk
```

Check the installation:

```bash
cds --version
```

If the version is shown, the CAP CLI is installed successfully.

---

## SQLite Database Setup

Sometimes the project starts but gives an error related to the database or says that no database driver/connection is available.

For local development, I use **SQLite** because CAP can run it locally without setting up a separate database server.

### Step 1: Install SQLite

From the project directory, run:

```bash
npm add @cap-js/sqlite -D
```

This adds the SQLite support required by the project.

If you are working with an older CAP release, you may need:
> npm add sqlite3 -D


### Step 2: Add SQLite Configuration

Run:

```bash
cds add sqlite
```

This adds the SQLite database configuration to the project.

### Step 3: Restart `cds watch`

If `cds watch` is already running, stop it:

```text
Ctrl + C
```

Then start it again:

```bash
cds watch
```

CAP will use an in-memory SQLite database for local development.

The database is typically created in memory using:

```text
:memory:
```

CAP also deploys the CDS database model and loads mock data when it is available.

For example:

```text
db/
├── schema.cds
└── data/
    └── ...
```

So for local development, I don't need to manually create a separate database server just to test the application.

---

## Create a New CAP Project

### 1. Initialize

```bash
cds init my-cap-project
cd my-cap-project
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Add SQLite

```bash
npm add @cap-js/sqlite -D
cds add sqlite
```

### 4. Start the Project

```bash
cds watch
```

The application should now be available at:

```text
http://localhost:4004
```

---

## Project Structure

```text
my-cap-project/
├── app/       # UI applications
├── db/        # Database models and mock data
└── srv/       # Services and business logic
```

A simple database setup can look like:

```text
db/
├── schema.cds
└── data/
    └── ...
```

---

---

## Mock Data with CSV

During development, I can use CSV files to add sample/mock data to the SQLite database.

### Step 1: Generate Mock Data Files

After creating the entity in `db/schema.cds`, run:

```bash
cds add data
```
This generates CSV files for the entities.

For example:

db/<br>
├── schema.cds<br>
└── data/<br>
    └── my.bookshop-Books.csv

The CSV file contains the columns based on the entity defined in schema.cds.
```bash
ID,title,author
1,The Alchemist,Paulo Coelho
2,Atomic Habits,James Clear
3,Clean Code,Robert C. Martin
```
For larger datasets, I can use GPT to generate realistic sample data according to the entity fields and then paste that data into the generated CSV file.

For example, I can ask GPT:
```bash
Generate 20 realistic records for this CAP entity in CSV format. Keep the column names exactly the same and make sure the IDs are unique.
```
Then copy the generated CSV data into:
```bash
db/data/
```
### So the basic workflow is:

```bash
schema.cds
    ↓
cds add data
    ↓
CSV files generated
    ↓
Fill CSV with sample data
    ↓
GPT can generate realistic CSV data
    ↓
Save CSV inside db/data/
    ↓
cds watch
    ↓
Mock data loaded into SQLite
```

## Useful Commands

| Command | What it does |
|---|---|
| `cds watch` | Starts the CAP development server |
| `cds init <project>` | Creates a new CAP project |
| `cds --version` | Shows the installed CAP CLI version |
| `npm install` | Installs project dependencies |
| `npm add @cap-js/sqlite -D` | Adds SQLite support |
| `cds add sqlite` | Adds SQLite database configuration |



## Quick Setup

For a fresh setup, these are the commands I need:

```bash
mkdir -p ~/.npm-global
npm config set prefix ~/.npm-global
echo 'export PATH="$HOME/.npm-global/bin:$PATH"' >> ~/.zshrc
source ~/.zshrc

npm i -g @sap/cds-dk

cds --version

cds init my-cap-project
cd my-cap-project

npm install
npm add @cap-js/sqlite -D
cds add sqlite

cds watch
```

Then open:

```text
http://localhost:4004
```

That's enough to get a basic **CAP + Node.js + SQLite** project running locally.

---

## Drafted by

Md. Azad | Linkedin : @themdazad
https://www.linkedin.com/in/themdazad/