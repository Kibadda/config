#!/bin/sh

socket="$XDG_RUNTIME_DIR/yubikey-touch-detector.socket"

while true; do
  if [ ! -e "$socket" ]; then
    printf '{"text": "Waiting for Yubikey socket"}\n'
    while [ ! -e "$socket" ]; do sleep 1; done
  fi

  printf '{"text": ""}\n'

  nc -U "$socket" | while read -n5 cmd; do
    if  [ $(echo $cmd | cut -d'_' -f2) = "1" ]; then
      printf '{"text": "🔑 Yubikey 🔑"}\n'
    else
      printf '{"text": ""}\n'
    fi
  done

  sleep 1
done
