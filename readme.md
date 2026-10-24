# Linux Prefetch Optimizer

A high-performance file access monitoring and prediction tool for Linux systems. This project uses `inotify` to track real-time file access patterns and predicts future access to prefetch files into memory, reducing latency for frequent operations.

## Features

- **Recursive Monitoring**: Tracks file access across multiple directories (excluding hidden system folders).
- **Deduplication Logic**: Intelligent filtering of redundant access events within a short time window.
- **Access Prediction**: Analyzes history logs to identify the most frequently accessed files.
- **Prefetching**: Pre-loads predicted files to improve system responsiveness.

## Components

- `main.c`: The central CLI entry point with menu options.
- `monitor.c`: Handles `inotify` setup and recursive directory watching.
- `predict.c`: Implements the frequency-based prediction algorithm.
- `prefetch.c`: Manages the loading of files into system cache.
- `makefile.txt`: Build system for the project.

## Installation & Usage

### Prerequisites
- Linux Environment (e.g., Kali, Ubuntu)
- GCC Compiler
- Inotify tools (kernel support)

### Build
To compile the project, use the provided makefile:
```bash
make -f makefile.txt
```

### Run
Launch the optimizer:
```bash
./prefetcher
```

## How it Works

1. **Monitor**: The tool watches `/home/kali` (configurable) for file open events.
2. **Log**: Access events are logged to `/tmp/history.log` after deduplication.
3. **Predict**: When requested, the tool scans the history to find the "hottest" file.
4. **Prefetch**: The predicted file is read to ensure it resides in the OS page cache.


