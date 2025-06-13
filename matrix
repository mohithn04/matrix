#!/usr/bin/env bash
set -euo pipefail

init_term() {
    printf '\e[?1049h\e[2J\e[?25l'
    if [ "${BASH_VERSINFO[0]:-0}" -le 3 ]; then
        read -r LINES COLUMNS < <(stty size)
    else
        shopt -s checkwinsize
        # Force a command to update LINES/COLUMNS
        (:)
    fi
}

deinit_term() { 
    # Kill all background jobs
    jobs -p | xargs -r kill 2>/dev/null || true
    printf '\e[?1049l\e[?25h'
    stty echo
}

print_to() {
    printf '\e[%d;%dH\e[32m%s\e[0m' "$2" "$3" "$1"
}

rain() {
    local dropStart dropCol dropLen dropSpeed dropColDim color symbol i
    
    ((dropStart = RANDOM % (LINES / 9 + 1)))
    ((dropCol = RANDOM % COLUMNS + 1))
    ((dropLen = RANDOM % (LINES * 3/4) + 10))
    ((dropSpeed = RANDOM % 9 + 1))
    ((dropColDim = RANDOM % 4))
    
    color="${COLORS[RANDOM % ${#COLORS[@]}]}"
    
    for ((i = dropStart; i <= LINES + dropLen; i++)); do
        symbol="${1:$((RANDOM % ${#1})):1}"
        
        # Draw bright character at current position
        if ((dropColDim == 0)) && ((i <= LINES)); then
            print_to "$symbol" "$i" "$dropCol"
        fi
        
        # Draw normal character at previous position
        if ((i > dropStart)) && ((i - 1 <= LINES)); then
            print_to "$symbol" "$((i-1))" "$dropCol"
        fi
        
        # Clear tail
        if ((i > dropLen)) && ((i - dropLen <= LINES)); then
            printf '\e[%d;%dH ' "$((i - dropLen))" "$dropCol"
        fi
        
        sleep "0.0$dropSpeed"
    done
}

cleanup() {
    deinit_term
    exit 0
}

trap cleanup EXIT INT TERM
trap 'init_term' WINCH

# Use a mix of characters for better compatibility
SYMBOLS='アイウエオカキクケコサシスセソタチツテトナニヌネノハヒフヘホマミムメモヤユヨラリルレロワヲン0123456789!@#$%^&*()-_=+[]{}|;:,.<>?abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ'
COLORS=('102;255;102')

matrix() {
    if ! init_term; then
        printf 'Failed initializing terminal\n' >&2
        return 1
    fi
    stty -echo
    
    local max_jobs=$((COLUMNS / 2))
    
    while true; do
        # Launch new raindrops
        for ((j = 0; j < 3; j++)); do
            rain "$SYMBOLS" &
        done
        
        # Simple job control to prevent too many background processes
        while (($(jobs -r | wc -l) > max_jobs)); do
            sleep 0.05
        done
        
        sleep 0.1
    done
}

matrix
