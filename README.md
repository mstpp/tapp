# Tap App 🔔

A simple, lightweight backend application for tracking daily actions through quick "taps" or signals. Perfect for anyone who needs a reliable memory aid for routine tasks.

## 🎯 Purpose

Tap App helps users maintain awareness of completed actions throughout their day. Whether it's medication reminders, habit tracking, or simple task completion logging, Tap provides a frictionless way to record and verify that important actions have been taken.

### Primary Use Case

The app serves as a digital memory aid, particularly valuable for:
- **Elderly users** who may struggle with short-term memory
- **Medication adherence** - verify doses were taken
- **Habit tracking** - confirm daily routines were completed
- **Task verification** - quick proof that an action was done

The core assumption: *If a user remembers to tap after performing an action, they'll never doubt whether they did it.*

## ✨ Features

### Core Functionality

- **Quick Tap**: Send an instant tap/signal with optional comment
  ```
  tap "Took morning medication"
  tap --comment "Watered plants"
  tap  # Simple tap without comment
  ```

- **History View**: Check previous taps with timestamps
  ```
  history --today
  history --last 10
  history --date 2024-03-15
  ```

- **Info & Help**: Display usage information and statistics
  ```
  info     # Show today's tap count and recent activity
  help     # Display available commands
  ```

### Extended Features (Future Enhancements)

- **Categories/Tags**: Organize taps by type
  ```
  tap "Morning vitamins" --category medication
  ```

- **Recurring Reminders**: Get notified if expected tap is missing
  ```
  remind --daily "morning meds" --at 09:00
  ```

- **Statistics**: View patterns and compliance rates
  ```
  stats --category medication --period week
  ```

- **Multiple Users**: Support for household/caregiver access
  ```
  tap "Patient took insulin" --user john
  ```

## 🏗️ Architecture

### Tech Stack

- **Language**: Rust (for learning and performance)
- **Storage**: SQLite for local persistence
- **API**: RESTful endpoints
- **CLI**: Optional command-line interface

### Data Model

```rust
struct Tap {
    id: i64,
    timestamp: DateTime<Utc>,
    comment: Option<String>,
    category: Option<String>,
    user_id: Option<i64>,
}
```

### API Endpoints

```
POST   /tap              Create a new tap
GET    /taps             List taps with filters
GET    /taps/:id         Get specific tap
DELETE /taps/:id         Delete a tap
GET    /stats            Get statistics
GET    /health           Health check
```

## 🚀 Getting Started

### Prerequisites

- Rust 1.70+ installed
- SQLite3

### Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/tap-app.git
cd tap-app

# Build the project
cargo build --release

# Run the server
cargo run --release
```

### Quick Start

```bash
# Start the server
./target/release/tap-app

# Send your first tap
curl -X POST http://localhost:8080/tap \
  -H "Content-Type: application/json" \
  -d '{"comment": "Took morning pills"}'

# View your history
curl http://localhost:8080/taps?today=true
```

## 📊 Example Usage Scenarios

### Medication Management

```bash
# Morning routine
tap "8:00 AM - Blood pressure pill"
tap "8:00 AM - Vitamin D"

# Evening check
history --today  # Verify both doses were logged
```

### Habit Tracking

```bash
# Daily habits
tap "Morning walk - 30 minutes"
tap "Drank 8 glasses of water"
tap "Called mom"

# Weekly review
stats --period week  # See consistency
```

### Caregiver Use

```bash
# Nurse logs patient activities
tap "Patient took insulin" --user patient_123
tap "Blood sugar check: 120" --user patient_123

# Family member checks remotely
history --user patient_123 --today
```

## 🔧 Configuration

Create a `config.toml` file:

```toml
[server]
host = "127.0.0.1"
port = 8080

[database]
path = "./tap_history.db"

[features]
enable_reminders = false
enable_categories = true
max_history_days = 365
```

## 🧪 Testing

```bash
# Run all tests
cargo test

# Run with coverage
cargo tarpaulin --out Html
```

## 📝 Development Roadmap

- [x] Basic tap creation and storage
- [x] History retrieval with filters
- [ ] Category/tag support
- [ ] Web UI for elderly users (large buttons, simple interface)
- [ ] Mobile app companion
- [ ] Reminder system
- [ ] Multi-user support
- [ ] Data export (CSV, JSON)
- [ ] Cloud sync option

## 🤝 Contributing

This is a learning project, but contributions are welcome! Please feel free to:
- Report bugs
- Suggest features
- Submit pull requests
- Improve documentation

## 📄 License

MIT License - feel free to use this for your own learning or projects.

## 🙏 Acknowledgments

Built as a Rust learning project with a practical purpose - helping people maintain independence and peace of mind in their daily routines.

---

**Note**: This app is a memory aid tool and should not replace medical advice or proper medication management systems. Always consult healthcare professionals for medical needs.