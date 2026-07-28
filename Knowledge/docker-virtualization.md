---
# Knowledge Frontmatter (required)
id: docker-virtualization
title: Docker 컨테이너 = 격리된 host process (namespaces + cgroups)
category: concept
mastery_level: L4
source: "https://man7.org/linux/man-pages/man7/namespaces.7.html ; https://man7.org/linux/man-pages/man7/cgroups.7.html (핵심 사실); 통합 서술은 dialogue에서 학습자 추론으로 도출"
verified: true
authored_by: learner
updated: 2026-07-28
related_skills: [file-based-socratic-dialogue, web-grounded-verification]
provenance: dialogue/docker-virtualization.md
---

# Docker 컨테이너 = 격리된 host process (namespaces + cgroups)

## 1. Claim (Verified Fact)
Docker container는 별도의 OS/kernel을 가상화한 것이 아니라, **host의 단 하나의 kernel을 공유하며 그 위에서 실행되는 평범한 host process**이다. 일반 process와의 차이는 오직 두 가지 kernel 기능뿐이다 — **namespaces**(PID·mount·network·UTS(hostname)·IPC·user 등 전역 자원마다 "격리된 뷰"를 제공)와 **cgroups**(그 process 그룹이 쓸 수 있는 CPU·메모리 등 자원의 **양**을 제한·측정). 이미지별로 다른 것은 kernel이 아니라 **userspace(rootfs: libc·바이너리·distro 파일)**뿐이다.

## 2. Why It's True (Grounding)
- **namespace** (source: man7.org namespaces(7)): *"A namespace wraps a global system resource in an abstraction that makes it appear to the processes within the namespace that they have their own isolated instance of the global resource."* 종류: Mount, PID, UTS(hostname), Network, IPC, User, Cgroup, Time.
- **cgroups** (source: man7.org cgroups(7)): *"a Linux kernel feature which allow processes to be organized into hierarchical groups whose usage of various types of resources can then be limited and monitored."*
- **반례로 확인된 사실 (일반 CS 원리):** `chroot`는 filesystem 루트(= Mount 격리 하나)만 바꾸므로, `chroot`된 process도 host의 전체 PID를 그대로 보고 host hostname을 그대로 쓴다. 즉 **filesystem 격리 ≠ 완전한 격리** → PID·hostname·network 등은 *각각의 namespace*로 따로 격리해야 한다.
- **왜 이미지별 OS가 되는가:** 모든 Linux 이미지(ubuntu/alpine…)는 host의 동일 kernel과 동일 **syscall ABI**를 공유하고, 다른 것은 rootfs에 준비된 userspace 파일들뿐이다. 그래서 서로 다른 배포판 이미지가 한 host 위에서 동시에 돈다.

## 3. Boundary Conditions
- **Holds when:** container의 target kernel ABI = host kernel ABI (예: Linux 이미지 on Linux host).
- **Breaks when:** ABI가 다를 때. **Windows 이미지는 Linux host kernel에서 그대로 못 돈다** — Windows 바이너리는 완전히 다른 kernel의 다른 syscall 집합을 기대하기 때문. (그래서 Docker Desktop on Mac/Windows는 내부적으로 Linux VM을 띄운다.)
- **VM과의 대비:** VM은 hypervisor로 **가상 하드웨어 + 별도 OS/kernel**을 통째로 올린다(강한 격리·큰 비용). container는 kernel을 공유하고 namespaces/cgroups로만 격리한다(가벼움·kernel 공유 리스크).

## 4. Connections (Relational)
- **일반 원리:** container = host 위의, **namespaces**로 뷰가 격리되고 **cgroups**로 자원이 제한된, 그냥 하나의 process. "가상화의 경계를 *하드웨어/OS*에 긋느냐(VM) vs. *process의 자원 뷰*에 긋느냐(container)"의 차이.
- Relates to: **`chroot`** — Mount namespace의 원시적 선조(filesystem 격리 only).
- Relates to: **syscall ABI** — 이미지별 OS 지원과 cross-OS 불가의 근본 원인.

## 5. Transfer (L4 Marker)
> **"전역 자원을 각 소비자에게 자기만의 격리된 인스턴스처럼 보여준다"**는 발상은 도메인을 넘나든다:
> - **namespace**: PID/mount/hostname 등 전역 kernel 자원 → 각 container에게 자기 것처럼.
> - **virtual memory**: 물리 메모리(전역 자원) → 각 process에게 "전체 주소공간이 내 것"처럼.
>
> 둘은 **같은 추상**이되 **구현 계층이 다르다**: virtual memory는 MMU·page table의 *주소 변환*으로, namespace는 자원별 *식별자 테이블 분리*로 실현한다. (학습자 통찰)

## 6. Provenance
- **Reached via:** Gate 3 (Articulate) on 2026-07-28
- **Verified at:** Gate 2 by 학습자(대화 전반 추론 확인) + 핵심 사실은 man7.org 인용
- **Dialogue:** dialogue/docker-virtualization.md
- **Original learner articulation:** "container는 프로세스다. 같은 host kernel의 syscall을 쓴다는 점은 동일하고, 차이는 cgroup으로 자원의 양을 한정하고 namespace로 자원식별자 테이블(PID·MNT·NET·UTS·IPC·USER)을 따로 관리해 '격리되어 보이는 것처럼' 하는 것. 이는 virtual memory가 물리 메모리를 프로세스마다 자기 것처럼 보여주는 것과 같은 발상이며, 구현(주소 변환 vs. 식별자 테이블 분리)만 다르다."
