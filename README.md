name: Song Download Command

on:
  workflow_dispatch:  # Manual trigger
    inputs:
      song_name:
        description: 'Name of the song to download'
        required: true

jobs:
  download-song:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.x'

      - name: Install Dependencies
        run: |
          pip install yt-dlp

      - name: Download Song
        run: |
          echo "${{ github.event.inputs.song_name }}" > song_name.txt
          python download_song.py "$(cat song_name.txt)"
