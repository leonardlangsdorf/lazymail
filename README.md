# LazyMail

The goal of LazyMail is to have a high quality email client on the terminal.

Email is a communication tool and the goal of LazyMail is to make it easy to communicate while eliminating the announces associated with communication. Ideally LazyMail would be like Neovim where the community can come together and create plugins to add features. Email is like any other text editing function.

I am inspired by the amazing work done by https://github.com/jesseduffield and his LazyGit and LazyDocker work that has made my life measurable better.

### Features

LazyMail a robust, user-friendly, and efficient terminal-based mail client, here are the key features it should have:

### **1. Core Features:**

#### **Account Management:**

- **Multiple Account Support:** Allow users to add, configure, and manage multiple email accounts (IMAP, SMTP) easily.
- **OAuth2 Integration:** Especially for services like Gmail and Outlook, to avoid needing users to store plain-text passwords.
- **Unified Inbox:** Show emails from all accounts in a single view or allow users to toggle between accounts.

#### **Email Management:**

- **Read, Reply, Compose, Forward:** Users should be able to easily perform all common email actions (e.g., reply to all, reply to sender, forward email).
- **Drafts Support:** Users can compose and save emails as drafts, with the ability to resume later.
- **Delete, Archive, Mark as Read/Unread:** Support standard email actions for efficient inbox management.
- **Move to Folder:** Ability to organize emails by moving them to different folders (e.g., "Work," "Personal").

#### **Search and Filters:**

- **Email Search:** Implement full-text search to find emails quickly. Provide options to filter by date, sender, subject, etc.
- **Custom Filters:** Users can create filters that automatically categorize or highlight emails based on specific conditions (e.g., from certain senders, with attachments).

#### **Attachments:**

- **Download Attachments:** Users should be able to download attachments directly from the terminal to their local file system.
- **Send Attachments:** Support for attaching files while composing emails.

#### **Keyboard Shortcuts:**

- **Keyboard-Driven UI:** Every action (e.g., navigate inbox, open email, reply, etc.) should have an efficient, user-friendly keyboard shortcut, inspired by tools like Vim, LazyGit, and Mutt.
- **Customizable Shortcuts:** Allow users to configure their own shortcuts.

### **2. Advanced Features:**

#### **Offline Support:**

- **Offline Access:** Cached emails that were previously fetched should be available for offline reading, with the ability to compose emails offline and send them when connected.

#### **Notification System:**

- **Terminal Notifications:** Alert users to new emails while they are using the terminal for other tasks.
- **External Notifications:** Support integration with desktop notifications (e.g., `notify-send` on Linux or `terminal-notifier` on macOS).

#### **Threaded Conversations:**

- **Email Threading:** Group related emails (replies, forwards) into a conversation or thread view for easy navigation and context.

#### **Spam and Junk Filtering:**

- **Custom Spam Filters:** Let users manually mark emails as spam or implement basic spam detection with IMAP's spam folder support.

#### **Custom Email Signatures:**

- **Per Account Signatures:** Allow users to create and customize signatures for each account.

### **3. UI and Customization:**

#### **Terminal UI Customization:**

- **Themes:** Allow users to choose different themes for the terminal interface (light, dark, or customized color schemes).
- **Terminal UI Layout:** Users can choose how their screen is laid out (e.g., a three-panel view with folders, email list, and the selected email).

#### **Custom Folders and Labels:**

- **Label Support:** Use color-coded or text labels to tag and organize emails.
- **Custom Folders:** Let users create and manage their own folder structures for different email categories.

### **4. Security and Privacy:**

#### **Encryption and Security:**

- **PGP/GPG Integration:** Enable encrypted email communication via OpenPGP or GPG for users who require secure email.
- **2FA (Two-Factor Authentication):** Allow the use of two-factor authentication for login where possible.

#### **Email Syncing Frequency Control:**

- **Control Sync Frequency:** Users can control how often the app checks for new mail, from manual refresh to auto-sync at set intervals.

### **5. Performance and Usability:**

#### **Performance Optimization:**

- **Minimal Resource Usage:** Keep memory and CPU usage low, ensuring fast email retrieval and management.
- **Fast Loading:** Emails and attachments should load quickly, even for large inboxes.

#### **Customizable Settings:**

- **Configurable Settings via File:** Allow users to manage settings (e.g., email sync frequency, shortcuts, layout) in a config file (JSON, YAML, or TOML).

#### **Error Handling and Logging:**

- **Clear Error Messages:** Provide useful, detailed error messages for failed actions like sending emails or connecting to an account.
- **Activity Log:** Option to enable a log file that tracks actions (e.g., connection attempts, email sent/received) for debugging purposes.

### **6. Integration and Extensibility:**

#### **Plugin Support (Future):**

- **Plugin System:** Design LazyMail to be extensible via plugins so users can add their own custom functionality (e.g., adding email reminders, calendar integration, etc.).

#### **External Tools Integration:**

- **Task Managers & Note Taking:** Option to integrate with task management tools (e.g., Todo.txt) or note-taking apps (e.g., markdown-based note systems).
- **CLI Tools:** Allow external CLI tools to interact with LazyMail (e.g., use `notmuch` or `mbsync` to sync emails).

### **7. Collaboration:**

#### **Sharing Features:**

- **Email Forwarding:** Easily forward messages.
- **Email Snippet Export:** Allow exporting of email content to external files for sharing, integration with task management systems, or archiving.

By covering the core and advanced features listed above, you can build an email client that appeals to power users and developers who prefer the efficiency of terminal-based workflows. Would you like help outlining the architecture for implementing any of these features?

# LazyMail Go Project Structure and Packages

## Project Structure

```
lazymail/
├── cmd/
│   └── lazymail/
│       └── main.go           # Application entry point
├── internal/
│   ├── ui/                   # UI-related packages
│   ├── email/                # Email handling packages
│   ├── config/               # Configuration handling
│   └── plugin/               # Plugin system implementation
├── pkg/                      # Packages that could be used by external projects
│   └── utils/                # Utility functions
├── scripts/                  # Lua scripts and plugins
│   ├── core/                 # Core Lua modules
│   │   ├── init.lua          # Main Lua entry point
│   │   ├── config.lua        # Default configuration
│   │   └── utils.lua         # Utility functions
│   └── plugins/              # User and community plugins
├── configs/                  # Configuration files
│   └── config.lua            # Main config file (Lua)
├── docs/                     # Documentation
├── test/                     # Test files
└── go.mod                    # Go module file
```

## Key Go Packages for Email and OAuth

1. Email Handling:

   - `github.com/emersion/go-imap`: IMAP client library
   - `github.com/emersion/go-message`: Email message parsing and formatting
   - `github.com/emersion/go-sasl`: SASL authentication for IMAP and SMTP
   - `github.com/go-mail/mail`: Easy email sending

2. OAuth and Authentication:

   - `golang.org/x/oauth2`: OAuth 2.0 client implementation

3. Terminal UI:

   - `github.com/rivo/tview`: Terminal UI library with a rich set of widgets
   - `github.com/gdamore/tcell/v2`: Low-level terminal interface library

4. Lua Integration:

   - `github.com/yuin/gopher-lua`: Lua VM implementation in Go
   - `github.com/layeh/gopher-luar`: Custom type reflection for gopher-lua

5. Auxiliary Packages:
   - `github.com/spf13/viper`: Configuration solution for Go applications
   - `github.com/sirupsen/logrus`: Structured logger for Go
   - `github.com/mattn/go-sqlite3`: SQLite driver for Go (for local data storage)

## Implementation Approach

1. Core Application (Go):

   - Implement the main application logic, UI rendering, and email protocols in Go.
   - Use `tview` for the terminal interface.
   - Implement a Lua VM integration using `gopher-lua` and `gopher-luar`.

2. Plugin System (Lua):

   - Design a plugin API that allows Lua scripts to interact with the core application.
   - Use `gopher-lua` to execute Lua plugins and `gopher-luar` to expose Go functions to Lua.

3. Configuration:

   - Use `viper` for configuration management, supporting both Go and Lua-based configs.

4. Email Handling:

   - Use `go-imap` for IMAP operations and `go-mail/mail` for sending emails.
   - Implement OAuth2 authentication using `golang.org/x/oauth2`.

5. User Interface:
   - Build the UI using `tview`, creating a modular design that can be easily customized.
   - Implement a keybinding system similar to LazyGit and LazyDocker.
