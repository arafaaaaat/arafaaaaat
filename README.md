<div align="center">
  <img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=26&duration=3000&pause=1000&color=0366D6&center=true&vCenter=true&width=650&lines=Systems+Programming;Kernel+Development;High-Performance+Computing+(HPC)+%26+Kernels" alt="Typing SVG" />
  
  <h3>Operating at Ring 0 and the raw hardware boundary</h3>
</div>

## About Me

Systems and kernel programmer specializing in low-level architecture, operating system internals, and bare-metal execution environments. My work focuses on building high-throughput inference engines, custom compute runtimes, and low-level kernel subsystems designed to extract deterministic performance directly from raw silicon.

```rust
use core::alloc::Layout;
use core::ptr;

#[repr(C, align(64))] // Cache-line aligned execution descriptor
pub struct Context {
    identity: *const u8,
    domains: [*const u8; 3],
    privilege_level: u8,
}

fn main() {
    unsafe {
        let layout = Layout::new::<Context>();
        let raw = std::alloc::alloc(layout) as *mut Context;
        
        if raw.is_null() {
            std::alloc::handle_alloc_error(layout);
        }

        // Direct memory mapping without safe abstractions
        ptr::addr_of_mut!((*raw).identity).write(b"Md. Yeasin Arafat\0".as_ptr());
        ptr::addr_of_mut!((*raw).domains).write([
            b"Kernel & OS Internals\0".as_ptr(),
            b"HPC & Compute Kernels\0".as_ptr(),
            b"Inference Runtimes & Execution Engines\0".as_ptr(),
        ]);
        ptr::addr_of_mut!((*raw).privilege_level).write(0); // Ring 0

        // Explicit heap deallocation
        std::alloc::dealloc(raw as *mut u8, layout);
    }
}
```

## Technical Focus

- **Inference Engines & Compute Runtimes**: Engineering low-overhead tensor execution runtimes, KV-cache memory managers, quantization kernels, and SIMD/vectorized operators.
- **Kernel & Operating System Internals**: Virtual memory layout, custom paging, interrupt handlers, zero-copy I/O pipelines, and POSIX/bare-metal abstractions.
- **High-Performance Computing (HPC)**: Cache-conscious architectures, low-level lock-free concurrency, compute kernel optimization, and memory hierarchy tuning.
- **Hardware-Software Boundary**: Squeezing peak IPC and throughput from bare silicon through hardware performance counters, memory bus saturation, and assembly tuning.

## Core Engineering

- ⚙️ Architecting custom high-performance inference engines and execution backends
- 🔬 Developing custom kernel modules, device drivers, and low-level memory controllers
- ⚡ Hand-tuning vectorized compute kernels (AVX-512, NEON) and hardware execution pipelines
- 🧩 Profiling microarchitectural bottlenecks, cache line thrashing, and memory subsystems

## Tools & Technologies

<div align="center">
  <img src="https://img.shields.io/badge/C-00599C?style=flat-square&logo=c&logoColor=white" height="20" alt="C"/>
  <img src="https://img.shields.io/badge/Rust-black?style=flat-square&logo=rust&logoColor=%23E57324" height="20" alt="Rust"/>
  <img src="https://img.shields.io/badge/Assembly-333333?style=flat-square&logo=assemblyscript&logoColor=white" height="20" alt="Assembly"/>
  <img src="https://img.shields.io/badge/Linux_Kernel-FCC624?style=flat-square&logo=linux&logoColor=black" height="20" alt="Linux Kernel"/>
  <img src="https://img.shields.io/badge/LLVM_/_Clang-262626?style=flat-square&logo=llvm&logoColor=white" height="20" alt="LLVM"/>
  <img src="https://img.shields.io/badge/Docker-2496ED?style=flat-square&logo=docker&logoColor=white" height="20" alt="Docker"/>
</div>
