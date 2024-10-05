---
title: 👩🏼‍🏫 Implementing Operating System Demand Paging
summary: It's the hardest task I've ever done;<
date: 2024-07-15
math: true
authors:
  - admin
tags:
  - OS
image:
  caption: 'Image credit: [**Unsplash**](https://unsplash.com)'
---
<style>
    body {
        text-align: justify; /* 양쪽 정렬 */
    }
</style>
### 주요 상수 및 구조체 정의

- **상수 정의**:
    - `PAGESIZE`: 각 페이지의 크기 (32 바이트).
    - `PAS_FRAMES`: 물리 메모리의 총 프레임 수 (256).
    - `PAS_SIZE`: 물리 메모리의 전체 크기 (8,192 바이트).
    - `VAS_PAGES`: 가상 메모리의 총 페이지 수 (64).
    - `VAS_SIZE`: 가상 메모리의 전체 크기 (2,048 바이트).
    - `PTE_SIZE`: 페이지 테이블 엔트리의 크기 (4 바이트).
    - `PAGETABLE_FRAMES`: 페이지 테이블에 필요한 프레임 수.
    - `PAGE_INVALID`, `PAGE_VALID`: 페이지 유효성 상태를 나타내는 플래그.
    - `MAX_REFERENCES`: 최대 참조 수 (256).
- **구조체 정의**:
    - `PageTableEntry`: 페이지 테이블 엔트리 구조체로 프레임 번호, 유효 플래그, 참조 횟수, 패딩을 포함.
    - `Process`: 각 프로세스를 나타내는 구조체로 프로세스 ID, 참조 길이, 참조 배열, 페이지 테이블, 할당된 프레임 수, 페이지 폴트 수, 참조된 횟수, 메모리 부족 플래그를 포함.

### 함수 정의

- **load_processes**:
    - 파일로부터 프로세스 정보를 읽어들여 `Process` 구조체 배열로 저장.
    - 프로세스 ID와 참조 길이를 읽고 참조 배열을 동적으로 할당 및 초기화.
    - 페이지 테이블 및 기타 변수들을 초기화.
    - 프로세스 배열의 크기를 동적으로 확장.
- **demand_paging**:
    - 각 프로세스가 참조하는 페이지를 물리 메모리에 매핑하고 페이지 폴트를 처리.
    - 자유 프레임 배열을 초기화하고 자유 프레임 인덱스를 설정.
    - 각 프로세스의 참조를 순차적으로 처리하며, 페이지가 유효하지 않으면 새로운 프레임을 할당.
    - 물리 메모리가 부족할 경우 메모리 부족 플래그를 설정.
    - 시뮬레이션이 끝난 후 각 프로세스의 상태를 출력.
- **main**:
    - 표준 입력으로부터 프로세스를 로드하고, `demand_paging` 함수를 호출하여 시뮬레이션을 수행.
    - 각 프로세스의 참조 배열을 해제하고 동적으로 할당된 프로세스 배열을 해제.

### 코드 설명

1. **프로세스 로드**:
    - 표준 입력으로부터 프로세스 정보를 읽어들이고 동적으로 `Process` 구조체를 할당.
    - 참조 배열을 파일로부터 읽어들여 각 프로세스에 저장.
2. **페이지 테이블 초기화**:
    - 각 프로세스의 페이지 테이블을 초기화하고 참조, 페이지 폴트 등의 변수를 초기화.
3. **Demand Paging 시뮬레이션**:
    - 각 프로세스의 페이지 참조를 처리하면서 페이지 테이블을 업데이트.
    - 페이지가 유효하지 않으면 자유 프레임을 할당하고 페이지 폴트를 기록.
    - 모든 참조를 처리한 후 각 프로세스의 페이지 테이블과 메모리 할당 상태를 출력.
4. **결과 출력**:
    - 각 프로세스의 할당된 프레임 수, 페이지 폴트 수, 참조된 횟수를 출력.
    - 총 할당된 프레임 수, 총 페이지 폴트 수, 총 참조 횟수를 출력.

   ### 주요 상수 및 구조체 정의

    - **상수 정의**:
        - `PAGESIZE`: 각 페이지의 크기 (32 바이트).
        - `PAS_FRAMES`: 물리 메모리의 총 프레임 수 (256).
        - `PAS_SIZE`: 물리 메모리의 전체 크기 (8,192 바이트).
        - `VAS_PAGES`: 가상 메모리의 총 페이지 수 (64).
        - `VAS_SIZE`: 가상 메모리의 전체 크기 (2,048 바이트).
        - `PTE_SIZE`: 페이지 테이블 엔트리의 크기 (4 바이트).
        - `PAGETABLE_FRAMES`: 페이지 테이블에 필요한 프레임 수.
        - `PAGE_INVALID`, `PAGE_VALID`: 페이지 유효성 상태를 나타내는 플래그.
        - `MAX_REFERENCES`: 최대 참조 수 (256).
        - `L1PT_ENTRIES`: 1레벨 페이지 테이블 엔트리 수 (8).
        - `L2PT_ENTRIES`: 2레벨 페이지 테이블 엔트리 수 (8).
        - `MAX_PROCESSES`: 최대 프로세스 수 (10).
    - **구조체 정의**:
        - `PageTableEntry`: 페이지 테이블 엔트리 구조체로 프레임 번호, 유효 플래그, 참조 횟수, 패딩을 포함.
        - `Process`: 각 프로세스를 나타내는 구조체로 프로세스 ID, 참조 길이, 참조 배열, 2단계 페이지 테이블, 할당된 프레임 수, 페이지 폴트 수, 참조된 횟수, 메모리 부족 플래그를 포함.

   ### 함수 정의

    - **load_processes**:
        - 파일로부터 프로세스 정보를 읽어들여 `Process` 구조체 배열로 저장.
        - 프로세스 ID와 참조 길이를 읽고 참조 배열을 동적으로 할당 및 초기화.
        - 1레벨 및 2레벨 페이지 테이블을 초기화.
    - **demand_paging**:
        - 각 프로세스가 참조하는 페이지를 물리 메모리에 매핑하고 페이지 폴트를 처리.
        - 자유 프레임 배열을 초기화하고 자유 프레임 인덱스를 설정.
        - 각 프로세스의 참조를 순차적으로 처리하며, 페이지가 유효하지 않으면 새로운 프레임을 할당.
        - 1레벨 페이지 테이블에 접근하여 필요시 2레벨 페이지 테이블을 할당.
        - 물리 메모리가 부족할 경우 메모리 부족 플래그를 설정.
        - 시뮬레이션이 끝난 후 각 프로세스의 상태를 출력.
    - **main**:
        - 표준 입력으로부터 프로세스를 로드하고, `demand_paging` 함수를 호출하여 시뮬레이션을 수행.
        - 각 프로세스의 페이지 테이블 및 참조 배열을 해제하고 동적으로 할당된 프로세스 배열을 해제.

   ### 코드 설명

    1. **프로세스 로드**:
        - 표준 입력으로부터 프로세스 정보를 읽어들이고 동적으로 `Process` 구조체를 할당.
        - 참조 배열을 파일로부터 읽어들여 각 프로세스에 저장.
        - 1레벨 및 2레벨 페이지 테이블을 초기화.
    2. **페이지 테이블 초기화**:
        - 각 프로세스의 1레벨 페이지 테이블을 동적 할당하고 2레벨 페이지 테이블을 위한 메모리도 동적 할당.
        - 페이지 테이블 엔트리를 초기화.
    3. **Demand Paging 시뮬레이션**:
        - 각 프로세스의 페이지 참조를 처리하면서 페이지 테이블을 업데이트.
        - 페이지가 유효하지 않으면 자유 프레임을 할당하고 페이지 폴트를 기록.
        - 1레벨 페이지 테이블 엔트리가 유효하지 않으면 새로운 프레임을 할당하고 2레벨 페이지 테이블을 동적 할당.
        - 모든 참조를 처리한 후 각 프로세스의 페이지 테이블과 메모리 할당 상태를 출력.
    4. **결과 출력**:
        - 각 프로세스의 할당된 프레임 수, 페이지 폴트 수, 참조된 횟수를 출력.
        - 1레벨 및 2레벨 페이지 테이블 매핑 상태를 출력.
        - 총 할당된 프레임 수, 총 페이지 폴트 수, 총 참조 횟수를 출력.

<3-1>

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// 상수 정의
#define PAGESIZE (32)       // 페이지 크기
#define PAS_FRAMES (256)    // 물리 메모리 프레임 수
#define PAS_SIZE (PAGESIZE * PAS_FRAMES)    // 물리 메모리 크기
#define VAS_PAGES (64)      // 가상 메모리 페이지 수
#define VAS_SIZE (PAGESIZE * VAS_PAGES)     // 가상 메모리 크기
#define PTE_SIZE (4)        // 페이지 테이블 엔트리 크기
#define PAGETABLE_FRAMES (VAS_PAGES * PTE_SIZE / PAGESIZE)  // 페이지 테이블에 필요한 프레임 수
#define PAGE_INVALID (0)    // 페이지가 유효하지 않음
#define PAGE_VALID (1)      // 페이지가 유효함
#define MAX_REFERENCES (256)    // 최대 참조 수

// 페이지 테이블 엔트리 구조체 정의
typedef struct {
    unsigned char frame;    // 프레임 번호
    unsigned char vflag;    // 유효 플래그
    unsigned char ref;      // 참조 횟수
    unsigned char pad;      // 패딩 (정렬)
} PageTableEntry;

// 프로세스 구조체 정의
typedef struct {
    int pid;    // 프로세스 아이디
    int ref_len;    // 참조 길이
    unsigned char *references;  // 참조 배열
    PageTableEntry page_table[VAS_PAGES]; // 페이지 테이블
    int allocated_frames;   // 할당된 프레임 수
    int page_faults;        // 페이지 폴트 수
    int references_made;    // 참조된 횟수
    int oom_flag;           // 메모리 부족 플래그
} Process;

// 파일로부터 프로세스 로드
void load_processes(FILE *file, Process **processes, int *num_processes) {
    int allocated_size = 10; // 초기 할당 크기
    *processes = malloc(allocated_size * sizeof(Process)); // 프로세스 배열 초기 할당
    *num_processes = 0; // 초기 프로세스 수

    while (1) {
        Process proc;
        // 파일에서 프로세스 ID 읽기
        if (fread(&proc.pid, sizeof(int), 1, file) != 1) break;
        // 파일에서 참조 길이 읽기
        if (fread(&proc.ref_len, sizeof(int), 1, file) != 1) break;

        // 참조 배열 메모리 할당
        proc.references = (unsigned char *)malloc(proc.ref_len * sizeof(unsigned char));
        // 파일에서 참조 배열 읽기
        if (fread(proc.references, sizeof(unsigned char), proc.ref_len, file) != proc.ref_len) {
            free(proc.references);  // 실패 시 메모리 해제
            break;
        }

        // 페이지 테이블 초기화
        memset(proc.page_table, 0, sizeof(proc.page_table));
        proc.allocated_frames = 0; // 할당된 프레임 수 초기화
        proc.page_faults = 0; // 페이지 폴트 수 초기화
        proc.references_made = 0; // 참조된 횟수 초기화
        proc.oom_flag = 0; // 메모리 부족 플래그 초기화

        (*processes)[(*num_processes)++] = proc; // 프로세스 배열에 추가

        // 배열이 가득 찼다면 크기 증가
        if (*num_processes >= allocated_size) {
            allocated_size *= 2;
            *processes = realloc(*processes, allocated_size * sizeof(Process));
        }
    }
}

// Demand paging 시뮬레이션
int demand_paging(Process *processes, int num_processes) {
    int total_allocated_frames = 0; // 총 할당된 프레임 수
    int total_page_faults = 0;      // 총 페이지 폴트 수
    int total_references = 0;       // 총 참조 횟수
    int free_frames[PAS_FRAMES];    // 자유 프레임 배열
    for (int i = 0; i < PAS_FRAMES; i++) {
        free_frames[i] = i;         // 초기 자유 프레임 설정
    }
    int free_frame_index = num_processes * 8; // 자유 프레임 인덱스 초기화
    int oom_flag = 0; // 메모리 부족 플래그

    //printf("Start() start\n");

    int max_references = 0;
    for (int i = 0; i < num_processes; i++) {
        if (processes[i].ref_len > max_references) {
            max_references = processes[i].ref_len;
        }
    }

    for (int ref = 0; ref < max_references; ref++) {
        for (int i = 0; i < num_processes; i++) {
            Process *proc = &processes[i];
            if (ref < proc->ref_len) {
                unsigned char page = proc->references[ref];
                PageTableEntry *entry = &proc->page_table[page];

                if (entry->vflag == PAGE_INVALID) {
                    if (free_frame_index >= PAS_FRAMES) {
                        oom_flag = 1;
                        proc->oom_flag = 1;
                        break;
                    }
                    int frame = free_frame_index++;
                    entry->frame = frame;
                    entry->vflag = PAGE_VALID;
                    entry->ref = 1;
                    proc->page_faults++;
                    proc->allocated_frames++;
                    total_allocated_frames++;
                    total_page_faults++;
                    //printf("[PID %02d REF:%03d] Page access %03d: PF,Allocated Frame %03d\n", proc->pid, ref, page, frame);
                } else {
                    entry->ref++;
                    //printf("[PID %02d REF:%03d] Page access %03d: Frame %03d\n", proc->pid, ref, page, entry->frame);
                }
                proc->references_made++;
                total_references++;
            }
        }
        if (oom_flag) {
            break;
        }
    }

    //printf("Start() end\n");

    if (oom_flag) {
        printf("Out of memory!!\n");
    }

    for (int i = 0; i < num_processes; i++) {
        Process *proc = &processes[i];
        printf("** Process %03d: Allocated Frames=%03d PageFaults/References=%03d/%03d\n",
               proc->pid, proc->allocated_frames+8, proc->page_faults, proc->references_made);

        for (int j = 0; j < VAS_PAGES; j++) {
            PageTableEntry *entry = &proc->page_table[j];
            if (entry->vflag == PAGE_VALID) {
                printf("%03d -> %03d REF=%03d\n", j, entry->frame, entry->ref);
            }
        }
    }

    printf("Total: Allocated Frames=%03d Page Faults/References=%03d/%03d\n",
           total_allocated_frames+8*num_processes, total_page_faults, total_references);

    return oom_flag;
}

int main() {
    Process *processes;
    int num_processes;

    load_processes(stdin, &processes, &num_processes);
    demand_paging(processes, num_processes);

    for (int i = 0; i < num_processes; i++) {
        free(processes[i].references);
    }
    free(processes);

    return 0;
}

```

<3-2>

```c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// 상수 정의
#define PAGESIZE (32)       // 페이지 크기
#define PAS_FRAMES (256)    // 물리 메모리 프레임 수
#define PAS_SIZE (PAGESIZE * PAS_FRAMES)    // 물리 메모리 크기
#define VAS_PAGES (64)      // 가상 메모리 페이지 수
#define VAS_SIZE (PAGESIZE * VAS_PAGES)     // 가상 메모리 크기
#define PTE_SIZE (4)        // 페이지 테이블 엔트리 크기
#define PAGETABLE_FRAMES (VAS_PAGES * PTE_SIZE / PAGESIZE)  // 페이지 테이블에 필요한 프레임 수
#define PAGE_INVALID (0)    // 페이지가 유효하지 않음
#define PAGE_VALID (1)      // 페이지가 유효함
#define MAX_REFERENCES (256)    // 최대 참조 수
#define L1PT_ENTRIES (8)    // 1레벨 페이지 테이블 엔트리 수
#define L2PT_ENTRIES (8)    // 2레벨 페이지 테이블 엔트리 수
#define MAX_PROCESSES (10)  // 최대 프로세스 수

// 페이지 테이블 엔트리 구조체 정의
typedef struct {
    unsigned char frame;    // 프레임 번호
    unsigned char vflag;    // 유효 플래그
    unsigned char ref;      // 참조 횟수
    unsigned char pad;      // 패딩 (정렬)
} PageTableEntry;

// 프로세스 구조체 정의
typedef struct {
    int pid;    // 프로세스 아이디
    int ref_len;    // 참조 길이
    unsigned char *references;  // 참조 배열
    PageTableEntry **l1_page_table; // 1레벨 페이지 테이블
    PageTableEntry ***l2_page_table; // 2레벨 페이지 테이블 배열
    int allocated_frames;   // 할당된 프레임 수
    int page_faults;        // 페이지 폴트 수
    int references_made;    // 참조된 횟수
    int oom_flag;           // 메모리 부족 플래그
} Process;

// 파일로부터 프로세스 로드
void load_processes(FILE *file, Process **processes, int *num_processes) {
    *processes = malloc(MAX_PROCESSES * sizeof(Process)); // 프로세스 배열 초기 할당
    *num_processes = 0; // 초기 프로세스 수

    while (*num_processes < MAX_PROCESSES) {
        Process proc;
        // 파일에서 프로세스 ID 읽기
        if (fread(&proc.pid, sizeof(int), 1, file) != 1) break;
        // 파일에서 참조 길이 읽기
        if (fread(&proc.ref_len, sizeof(int), 1, file) != 1) break;

        // 참조 배열 메모리 할당
        proc.references = (unsigned char *)malloc(proc.ref_len * sizeof(unsigned char));
        // 파일에서 참조 배열 읽기
        if (fread(proc.references, sizeof(unsigned char), proc.ref_len, file) != proc.ref_len) {
            free(proc.references);  // 실패 시 메모리 해제
            break;
        }

        // 1레벨 페이지 테이블 초기화
        proc.l1_page_table = (PageTableEntry **)calloc(L1PT_ENTRIES, sizeof(PageTableEntry *));
        // 2레벨 페이지 테이블 초기화
        proc.l2_page_table = (PageTableEntry ***)calloc(L1PT_ENTRIES, sizeof(PageTableEntry **));
        for (int i = 0; i < L1PT_ENTRIES; i++) {
            proc.l1_page_table[i] = NULL;
            proc.l2_page_table[i] = NULL;
        }
        proc.allocated_frames = 0; // 할당된 프레임 수 초기화
        proc.page_faults = 0; // 페이지 폴트 수 초기화
        proc.references_made = 0; // 참조된 횟수 초기화
        proc.oom_flag = 0; // 메모리 부족 플래그 초기화

        (*processes)[(*num_processes)++] = proc; // 프로세스 배열에 추가
    }
}

int demand_paging(Process *processes, int num_processes) {
    int total_allocated_frames = 0; // 총 할당된 프레임 수
    int total_page_faults = 0; // 총 페이지 폴트 
    int total_references = 0;       // 총 참조 횟수
    int free_frames[PAS_FRAMES];    // 자유 프레임 배열
    for (int i = 0; i < PAS_FRAMES; i++) {
        free_frames[i] = i;         // 초기 자유 프레임 설정
    }
    int free_frame_index = num_processes; // 초기 자유 프레임 인덱스
    int oom_flag = 0; // 메모리 부족 플래그

    int max_references = 0;
    for (int i = 0; i < num_processes; i++) {
        if (processes[i].ref_len > max_references) {
            max_references = processes[i].ref_len;
        }
    }

    for (int ref = 0; ref < max_references; ref++) {
        for (int i = 0; i < num_processes; i++) {
            Process *proc = &processes[i];
            if (ref < proc->ref_len) {
                unsigned char page = proc->references[ref];
                int l1_index = page / L2PT_ENTRIES;
                int l2_index = page % L2PT_ENTRIES;
                PageTableEntry *l1_entry;
                PageTableEntry *l2_entry;

                // 1레벨 페이지 테이블에 접근
                if (proc->l1_page_table[l1_index] == NULL) {
                    if (free_frame_index >= PAS_FRAMES) {
                        oom_flag = 1;
                        proc->oom_flag = 1;
                        break;
                    }
                    int frame = free_frames[free_frame_index++];
                    proc->l1_page_table[l1_index] = (PageTableEntry *)malloc(sizeof(PageTableEntry));
                    proc->l2_page_table[l1_index] = (PageTableEntry **)calloc(L2PT_ENTRIES, sizeof(PageTableEntry *));
                    proc->l1_page_table[l1_index]->frame = frame;
                    proc->l1_page_table[l1_index]->vflag = PAGE_VALID;
                    proc->l1_page_table[l1_index]->ref = 0;
                    proc->page_faults++;
                    proc->allocated_frames++;
                    total_allocated_frames++;
                    total_page_faults++;
                }

                l1_entry = proc->l1_page_table[l1_index];
                if (proc->l2_page_table[l1_index][l2_index] == NULL) {
                    if (free_frame_index >= PAS_FRAMES) {
                        oom_flag = 1;
                        proc->oom_flag = 1;
                        break;
                    }
                    int frame = free_frames[free_frame_index++];
                    proc->l2_page_table[l1_index][l2_index] = (PageTableEntry *)malloc(sizeof(PageTableEntry));
                    proc->l2_page_table[l1_index][l2_index]->frame = frame;
                    proc->l2_page_table[l1_index][l2_index]->vflag = PAGE_VALID;
                    proc->l2_page_table[l1_index][l2_index]->ref = 1;
                    proc->page_faults++;
                    proc->allocated_frames++;
                    total_allocated_frames++;
                    total_page_faults++;
                } else {
                    proc->l2_page_table[l1_index][l2_index]->ref++;
                }

                proc->references_made++;
                total_references++;
            }
        }
        if (oom_flag) {
            break;
        }
    }

    if (oom_flag) {
        printf("Out of memory!!\n");
    }

    for (int i = 0; i < num_processes; i++) {
        Process *proc = &processes[i];
        printf("** Process %03d: Allocated Frames=%03d PageFaults/References=%03d/%03d\n",
               proc->pid, proc->allocated_frames + 1, proc->page_faults, proc->references_made);

        for (int l1_index = 0; l1_index < L1PT_ENTRIES; l1_index++) {
            if (proc->l1_page_table[l1_index] != NULL) {
                printf("(L1PT) %03d -> %03d\n", l1_index, proc->l1_page_table[l1_index]->frame);
                for (int l2_index = 0; l2_index < L2PT_ENTRIES; l2_index++) {
                    if (proc->l2_page_table[l1_index][l2_index] != NULL) {
                        PageTableEntry *l2_entry = proc->l2_page_table[l1_index][l2_index];
                        if (l2_entry->vflag == PAGE_VALID) {
                            printf("(L2PT) %03d -> %03d REF=%03d\n", l1_index * L2PT_ENTRIES + l2_index, l2_entry->frame, l2_entry->ref);
                        }
                    }
                }
            }
        }
    }

    printf("Total: Allocated Frames=%03d Page Faults/References=%03d/%03d\n",
           total_allocated_frames + num_processes, total_page_faults, total_references);
    
    return oom_flag;
}

int main() {
    Process *processes;
    int num_processes;

    load_processes(stdin, &processes, &num_processes);
    demand_paging(processes, num_processes);

    for (int i = 0; i < num_processes; i++) {
        for (int j = 0; j < L1PT_ENTRIES; j++) {
            if (processes[i].l1_page_table[j] != NULL) {
                free(processes[i].l1_page_table[j]);
                for (int k = 0; k < L2PT_ENTRIES; k++) {
                    if (processes[i].l2_page_table[j][k] != NULL) {
                        free(processes[i].l2_page_table[j][k]);
                    }
                }
                free(processes[i].l2_page_table[j]);
            }
        }
        free(processes[i].l1_page_table);
        free(processes[i].l2_page_table);
        free(processes[i].references);
    }
    free(processes);

    return 0;
}

```
