# melange

<!---
Note: Do NOT edit directly, this file was generated using https://github.com/chainguard-images/readme-generator
-->

[![CI status](https://github.com/chainguard-images/melange/actions/workflows/release.yaml/badge.svg)](https://github.com/chainguard-images/melange/actions/workflows/release.yaml)

Container image for running [melange](https://github.com/chainguard-dev/melange) workflows to build APK packages.

## Get It!

The image is available on `cgr.dev`:

```
docker pull cgr.dev/chainguard/melange:latest
```

## Supported tags

| Tag | Digest | Arch |
| --- | ------ | ---- |
| `latest` `v0.1.0` | `sha256:1908627a7a3c8a50052d26e24769d58d0b539efcaa34e300a5ed40104859384b`<br/>[View entry in Rekor](https://rekor.tlog.dev/?hash=sha256:1908627a7a3c8a50052d26e24769d58d0b539efcaa34e300a5ed40104859384b) | `amd64` `arm64` `armv7` |


## Usage

To build the melange workflow in [examples](examples/gnu-hello.yaml):

```
docker run --privileged -v "$PWD":/work cgr.dev/chainguard/melange build /work/examples/gnu-hello.yaml
```

Output will be in the `packages` directory.

To build the melange package for the host architecture:

```
docker run --privileged -v "$PWD":/work cgr.dev/chainguard/melange build --empty-workspace --arch $(uname -m) /work/melange.yaml
```

To get a shell, you can change the entrypoint:

```
docker run --privileged -v "$PWD":/work -it --entrypoint /bin/sh cgr.dev/chainguard/melange

/ # melange version
...
```
Note that melange uses bubblewrap internally, which requires various Linux capabilities, hence the
use of `--privileged`. Because of this requirement, we recommend this image is used only for local
development and testing.


## Signing

All Chainguard Images are signed using [Sigstore](https://sigstore.dev)!

<details>
<br/>
To verify the image, download <a href="https://github.com/sigstore/cosign">cosign</a> and run:

```
COSIGN_EXPERIMENTAL=1 cosign verify cgr.dev/chainguard/melange:latest | jq
```

Output:
```
Verification for cgr.dev/chainguard/melange:latest --
The following checks were performed on each of these signatures:
  - The cosign claims were validated
  - Existence of the claims in the transparency log was verified offline
  - Any certificates were verified against the Fulcio roots.
[
  {
    "critical": {
      "identity": {
        "docker-reference": "ghcr.io/chainguard-images/melange"
      },
      "image": {
        "docker-manifest-digest": "sha256:1908627a7a3c8a50052d26e24769d58d0b539efcaa34e300a5ed40104859384b"
      },
      "type": "cosign container image signature"
    },
    "optional": {
      "1.3.6.1.4.1.57264.1.1": "https://token.actions.githubusercontent.com",
      "1.3.6.1.4.1.57264.1.2": "schedule",
      "1.3.6.1.4.1.57264.1.3": "7a9bfdb03ef9b75b8aaed41c3d0aafbfbfd589a0",
      "1.3.6.1.4.1.57264.1.4": "Create Release",
      "1.3.6.1.4.1.57264.1.5": "chainguard-images/melange",
      "1.3.6.1.4.1.57264.1.6": "refs/heads/main",
      "Bundle": {
        "SignedEntryTimestamp": "MEUCIGPGu94ycRf7Gy+ybEjunEQzJhxNPQyYjZSjUqSVp+qwAiEAov7WEHzf53Htz+RaVFpxGDLhRVMQgSyPtdT39wVC/+A=",
        "Payload": {
          "body": "eyJhcGlWZXJzaW9uIjoiMC4wLjEiLCJraW5kIjoiaGFzaGVkcmVrb3JkIiwic3BlYyI6eyJkYXRhIjp7Imhhc2giOnsiYWxnb3JpdGhtIjoic2hhMjU2IiwidmFsdWUiOiJhNjQzZmUwMjJiMWIyMWVmOTFiYzVlMDM4YTVjZDg1NzFjM2VhNTU0Mjc3MWU0ZjU4MzcxZmY4YTFkYWFkNjIyIn19LCJzaWduYXR1cmUiOnsiY29udGVudCI6Ik1FVUNJRlpIQ2lrRU1sVnlWaVFWNzhjNVdWaERRenozQU1JQ29vTVRMSnZ1M3V1QkFpRUFyU1RsaGRUdzRBRGluY3JBWWtTSVo3dWIrY290dU1GYlZxRG5YZjJzK2xJPSIsInB1YmxpY0tleSI6eyJjb250ZW50IjoiTFMwdExTMUNSVWRKVGlCRFJWSlVTVVpKUTBGVVJTMHRMUzB0Q2sxSlNVUnlWRU5EUVhwUFowRjNTVUpCWjBsVldHWm9aMHhxTmtwVGVqWTJibWx0ZWxFd00yWjRhRXhZVVUxUmQwTm5XVWxMYjFwSmVtb3dSVUYzVFhjS1RucEZWazFDVFVkQk1WVkZRMmhOVFdNeWJHNWpNMUoyWTIxVmRWcEhWakpOVWpSM1NFRlpSRlpSVVVSRmVGWjZZVmRrZW1SSE9YbGFVekZ3WW01U2JBcGpiVEZzV2tkc2FHUkhWWGRJYUdOT1RXcEplRTFFUlhsTlJFVjNUMFJOTVZkb1kwNU5ha2w0VFVSRmVVMUVSWGhQUkUweFYycEJRVTFHYTNkRmQxbElDa3R2V2tsNmFqQkRRVkZaU1V0dldrbDZhakJFUVZGalJGRm5RVVZhYWxweWEydEtUbVZoSzFCQ1RVNU1UMVZTVG5jMlNHMTZlbUl2Y1hRM1VsTldaRW9LVWxRM1VYSnZSaXRWVFdwbGMwdExSMjVLY2xWS2NuaFpkVk4yV25kaEszQnVkbk0wV1dGV1ZGSmlhRzFGTUdaTGNqWlBRMEZzU1hkblowcFBUVUUwUndwQk1WVmtSSGRGUWk5M1VVVkJkMGxJWjBSQlZFSm5UbFpJVTFWRlJFUkJTMEpuWjNKQ1owVkdRbEZqUkVGNlFXUkNaMDVXU0ZFMFJVWm5VVlYzYldwR0Nra3ZNbWxDVlRsaFRWSlFTRWRSTlZRdldsRkNhek5WZDBoM1dVUldVakJxUWtKbmQwWnZRVlV6T1ZCd2VqRlphMFZhWWpWeFRtcHdTMFpYYVhocE5Ga0tXa1E0ZDJGUldVUldVakJTUVZGSUwwSkdPSGRZV1ZwaVlVaFNNR05JVFRaTWVUbHVZVmhTYjJSWFNYVlpNamwwVERKT2IxbFhiSFZhTTFab1kyMVJkQXBoVnpGb1dqSldla3d5TVd4aVIwWjFXakpWZGt4dFpIQmtSMmd4V1drNU0ySXpTbkphYlhoMlpETk5kbU50Vm5OYVYwWjZXbE0xTlZsWE1YTlJTRXBzQ2xwdVRYWmhSMVpvV2toTmRtSlhSbkJpYWtFMVFtZHZja0puUlVWQldVOHZUVUZGUWtKRGRHOWtTRkozWTNwdmRrd3pVblpoTWxaMVRHMUdhbVJIYkhZS1ltNU5kVm95YkRCaFNGWnBaRmhPYkdOdFRuWmlibEpzWW01UmRWa3lPWFJOUWxsSFEybHpSMEZSVVVKbk56aDNRVkZKUlVOSVRtcGhSMVpyWkZkNGJBcE5SRmxIUTJselIwRlJVVUpuTnpoM1FWRk5SVXRFWkdoUFYwcHRXa2RKZDAweVZtMVBWMGt6VGxkSk5GbFhSbXhhUkZGNFdYcE9hMDFIUm1oYWJVcHRDbGx0V210T1ZHYzFXVlJCZDBoQldVdExkMWxDUWtGSFJIWjZRVUpDUVZGUFVUTktiRmxZVW14SlJrcHNZa2RXYUdNeVZYZEtkMWxMUzNkWlFrSkJSMFFLZG5wQlFrSlJVVnBaTW1ob1lWYzFibVJYUm5sYVF6RndZbGRHYmxwWVRYWmlWMVp6V1ZjMWJscFVRV1JDWjI5eVFtZEZSVUZaVHk5TlFVVkhRa0U1ZVFwYVYxcDZUREpvYkZsWFVucE1NakZvWVZjMGQyZFpiMGREYVhOSFFWRlJRakZ1YTBOQ1FVbEZaa0ZTTmtGSVowRmtaMEZKV1VwTWQwdEdUQzloUlZoU0NqQlhjMjVvU25oR1duaHBjMFpxTTBSUFRrcDBOWEozYVVKcVduWmpaMEZCUVZsUVNuWkliaTlCUVVGRlFYZENTRTFGVlVOSlEwbDBVbWxKUldadVprSUtXaTgzVmxRclltdHhWVWh0VFZGblVqaFFMelJRUzFwNU4zTlpaMkpJU2pSQmFVVkJPV1ZyUlZSTGVsaHhkU3RTU2pKRFRtTmFiSFF2UlhOd05FbzVid3AxTVZZd2JWUTBRa2x2ZVVNeU1UUjNRMmRaU1V0dldrbDZhakJGUVhkTlJHRkJRWGRhVVVsM1ZubFNhSG8zTjFkWWFVSnFhRUZIUWtWTFpHcFJLMnhOQ214WVJWRnFibGRXVkVKalZtbERjWE5rYVZveFoyMTFjMU5OU0doaVRHaE9PVEIwYUhsbFNuaEJha1ZCY0dzeWNETXZNREZ1VURkdGRUaGlTamR6ZERrS04yTllMMDV2WkN0RmEwZFNaVXN3YWpoRFVXUmFVbXN5ZVVGMGVVRXZjazlqYW0xaGRXczNibUo2U1RNS0xTMHRMUzFGVGtRZ1EwVlNWRWxHU1VOQlZFVXRMUzB0TFFvPSJ9fX19",
          "integratedTime": 1665536924,
          "logIndex": 4930275,
          "logID": "c0d23d6ad406973f9559f3ba2d1ca01f84147d8ffc5b8445c224f98b9591801d"
        }
      },
      "Issuer": "https://token.actions.githubusercontent.com",
      "Subject": "https://github.com/chainguard-images/melange/.github/workflows/release.yaml@refs/heads/main",
      "githubWorkflowName": "Create Release",
      "githubWorkflowRef": "refs/heads/main",
      "githubWorkflowRepository": "chainguard-images/melange",
      "githubWorkflowSha": "7a9bfdb03ef9b75b8aaed41c3d0aafbfbfd589a0",
      "githubWorkflowTrigger": "schedule",
      "run_attempt": "1",
      "run_id": "3231259727",
      "sha": "7a9bfdb03ef9b75b8aaed41c3d0aafbfbfd589a0"
    }
  }
]
```

You can verify that the image was built in Github Actions in this repository from the `Issuer` and `Subject` fields.
</details>

## Build

This image is built with [melange](https://github.com/chainguard-dev/melange) and [apko](https://github.com/chainguard-dev/apko).

