workflows/main.yml
name: MRX-ACTION
on:
  workflow_dispatch:
    inputs:
      ip:
        description: 'Target IP'
        required: true
      port:
        description: 'Target Port'
        required: true
      duration:
        description: 'Duration'
        required: true
      packet_size:
        description: 'Packet Size'
        required: true
      threads:
        description: 'Threads'
        required: true

jobs:
  run-mrx:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Code
        uses: actions/checkout@v2

      - name: Setup Environment
        run: |
          chmod +x mrx
          # main.py को रन करना जो बाइनरी फाइल mrx को चलाएगी
          python3 main.py ${{ github.event.inputs.ip }} ${{ github.event.inputs.port }} ${{ github.event.inputs.duration }} ${{ github.event.inputs.packet_size }} ${{ github.event.inputs.threads }}
          
