# Husky

The Husky hooks will perform certain actions before a specific task happens; for example, it can run a format command so all of my files get formatted automatically before they get committed.

First of all, we need to install Husky. So let's start by installing Husky. To install Husky Run the following command.

```bash
npm install husky --save-dev
```

Initialize husky for Git Hooks

```bash
npx husky init
```

Add a new script to your “package.json” file

```bash
"scripts": {
    "prepare": "husky"
}
```

Create a `.husky/pre-commit`

```bash
npx lint-staged
```

## Husky Pre Commit Template

Here’s an example folder structure where your ****Husky pre-commit script will work correctly:

```
/your-project-root
│── .git/                  # Git repository metadata (hidden)
│── .husky/                # Husky hooks (should not trigger lint-staged)
│   ├── pre-commit
│── frontend/              # Frontend directory (can be any name)
│   ├── package.json
│── backend/               # Backend directory (can be any name)
│   ├── package.json
│── package.json           # Root package.json
│── .gitignore
│── README.md

```

1. Dynamic for any folder structure like ( `client`, `server`, `frontend`, etc.) are used.

```powershell
# Get only staged (added) files
CHANGED_FILES=$(git diff --cached --name-only)

# Extract top-level directories, ignoring hidden/system directories
CHANGED_DIRS=$(echo "$CHANGED_FILES" | awk -F'/' '{print $1}' | sort -u | grep -E "^[a-zA-Z0-9_-]+$")

# Run lint-staged only inside changed directories
for DIR in $CHANGED_DIRS; do
  if [ -d "$DIR" ]; then
    echo "Running lint-staged for $DIR..."
    cd "$DIR"
    npx lint-staged --relative $(echo "$CHANGED_FILES" | grep "^$DIR/" | sed "s|^$DIR/||")
    cd ..
  fi
done
```

1. For specifie directory like ( `client`, `server` ) are used.

```powershell
# Get only staged (added) files
CHANGED_FILES=$(git diff --cached --name-only)

# Filter changed files for client and server
CLIENT_FILES=$(echo "$CHANGED_FILES" | grep "^client/" || true)
SERVER_FILES=$(echo "$CHANGED_FILES" | grep "^server/" || true)

# Run lint-staged only for client files
if [ -n "$CLIENT_FILES" ]; then
  echo "Running lint-staged for client files..."
  cd client
  npx lint-staged --relative $(echo "$CLIENT_FILES" | sed 's|^client/||')
  cd ..
fi

# Run lint-staged only for server files
if [ -n "$SERVER_FILES" ]; then
  echo "Running lint-staged for server files..."
  cd server
  npx lint-staged --relative $(echo "$SERVER_FILES" | sed 's|^server/||')
  cd ..
fi
```