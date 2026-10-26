# onnxruntime-intel-mac

Unofficial CPython wheels of [microsoft/onnxruntime](https://github.com/microsoft/onnxruntime) for Intel (x86_64) Macs.

Microsoft stopped publishing x86_64 macOS builds after onnxruntime 1.23.2 (which only covers CPython 3.10 to 3.13). Anything that needs a newer onnxruntime or CPython 3.14 on an Intel Mac, for example fastembed and the Mnemosyne memory plugin for Hermes Agent, cannot install from PyPI.

This repo builds the unmodified upstream source tag natively on GitHub's Intel macOS runner, smoke-tests the wheel with fastembed, and publishes it as a release with SHA-256 checksums. Nothing is patched.

## Use

Download the wheel from Releases, check it against `SHA256SUMS`, put it in a folder and point pip or uv at it:

```bash
pip install --find-links /path/to/folder onnxruntime==1.28.3
# or for uv
export UV_FIND_LINKS=/path/to/folder
```

## Build another version

Only the repo owner can start builds here. To build a different version yourself:

1. Fork this repo.
2. In your fork: Actions → "Build onnxruntime wheel (Intel macOS)" → Run workflow, then set the onnxruntime version, CPython version and minimum macOS.

It runs on your own account. Standard runners are free for public repos, so a public fork costs nothing. The wheel ends up in your fork's Releases.

## Notes

- Microsoft raised the official minimum to macOS 14 with 1.24. These builds target macOS 13.3 by default (13.3 is where Apple's C++ library gained the floating-point std::format support the source needs). That combination is not tested by Microsoft.
- onnxruntime is MIT licensed by Microsoft. License and third-party notices ship inside the wheel.
