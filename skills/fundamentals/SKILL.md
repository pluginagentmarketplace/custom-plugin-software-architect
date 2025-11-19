---
name: fundamentals
description: Master foundational computer science concepts, data structures, algorithms, Git/GitHub, programming languages (Rust, C++, Kotlin), and career development paths. Learn problem-solving, software design, and progress toward leadership roles.
---

# Fundamentals & Career Development Skill

## Quick Start

Build strong foundations in computer science and advance your career.

### Essential Path: Computer Science → Data Structures & Algorithms → System Design

```cpp
// C++ Data Structure: Binary Search Tree
#include <iostream>
using namespace std;

struct Node {
    int value;
    Node* left;
    Node* right;

    Node(int val) : value(val), left(nullptr), right(nullptr) {}
};

class BST {
public:
    Node* root;

    BST() : root(nullptr) {}

    void insert(int value) {
        if (root == nullptr) {
            root = new Node(value);
        } else {
            insertHelper(root, value);
        }
    }

private:
    void insertHelper(Node* node, int value) {
        if (value < node->value) {
            if (node->left == nullptr) {
                node->left = new Node(value);
            } else {
                insertHelper(node->left, value);
            }
        } else {
            if (node->right == nullptr) {
                node->right = new Node(value);
            } else {
                insertHelper(node->right, value);
            }
        }
    }
};
```

## What You'll Learn

### Foundations (Self-Paced, Critical for All)
- **Computer Science** - Theory, algorithms, complexity, paradigms
- **Data Structures** - Arrays, lists, trees, graphs, heaps
- **Algorithms** - Sorting, searching, dynamic programming
- **Complexity Analysis** - Big O notation, time/space tradeoffs

### Version Control Mastery
- **Git Fundamentals** - Commits, branches, merges, rebasing
- **GitHub Workflows** - Pull requests, code review, CI/CD
- **Collaboration** - Team workflows, conflict resolution

### Systems Programming (12-18 months)
- **Rust** - Memory safety, concurrency, performance (121 topics)
- **C++** - Object-oriented, performance, systems (127 topics)
- **Kotlin** - JVM language, Android, null safety

### Career Development Paths
- **QA Engineer** - Testing, quality assurance, automation
- **Technical Writer** - Documentation, communication, content
- **DevRel Engineer** - Community, advocacy, education
- **Engineering Manager** - Leadership, strategy, mentoring

## Key Topics

### Computer Science (188 topics)
1. **Complexity Analysis** - Big O, space, time tradeoffs
2. **Algorithms** - Sorting, searching, graph algorithms
3. **Data Structures** - Arrays, lists, stacks, queues, trees
4. **Design Patterns** - Creational, structural, behavioral
5. **SOLID Principles** - Single responsibility, open/closed
6. **Paradigms** - OOP, functional, declarative

### Data Structures & Algorithms (107 topics)
1. **Linear Structures** - Arrays, linked lists, stacks, queues
2. **Trees** - Binary trees, BST, balanced trees, heaps
3. **Graphs** - DFS, BFS, shortest path, minimum spanning tree
4. **Hashing** - Hash tables, collision resolution
5. **Dynamic Programming** - Memoization, tabulation
6. **Sorting** - Quick sort, merge sort, heap sort
7. **Searching** - Binary search, depth/breadth-first

### Git & GitHub (159 topics)
1. **Git Basics** - Init, add, commit, log, diff
2. **Branching** - Creating, switching, merging, rebasing
3. **Remote** - Clone, fetch, pull, push, tracking branches
4. **Advanced** - Cherry-pick, squash, rebase -i, bisect
5. **GitHub Features** - PRs, reviews, actions, pages, security
6. **Workflows** - Git Flow, GitHub Flow, trunk-based

### Rust Ecosystem (121 topics)
1. **Ownership & Borrowing** - Move semantics, lifetimes
2. **Error Handling** - Result, Option, custom errors
3. **Concurrency** - Threads, channels, async/await
4. **Systems Programming** - Memory management, FFI
5. **WebAssembly** - WASM compilation, browser usage
6. **Web Development** - Actix, Axum, Tauri

### C++ Ecosystem (127 topics)
1. **Core Language** - Objects, templates, modern C++
2. **Memory Management** - Pointers, smart pointers, RAII
3. **STL** - Containers, iterators, algorithms
4. **Advanced Features** - Concepts, constraints, ranges
5. **Performance** - SIMD, caching, profiling
6. **Game Development** - Unreal Engine, graphics

## Learning Outcomes

After completing this skill:

✅ Solve algorithmic problems
✅ Analyze code complexity
✅ Understand design patterns
✅ Master Git/GitHub workflows
✅ Build systems with Rust or C++
✅ Write efficient algorithms
✅ Design scalable architectures
✅ Lead technical teams
✅ Mentor junior developers
✅ Progress to leadership roles

## Learning Paths by Career Goal

### Path 1: Specialist Developer (2-5 years)
1. CS Fundamentals (3-6 months)
2. Data Structures & Algorithms (3-6 months)
3. Language Mastery - Rust/C++ (1-2 years)
4. Systems Design (1-2 years)
5. Thought Leadership

### Path 2: Engineering Manager (5-10 years)
1. Strong Technical Foundation (1-2 years)
2. Code Review & Mentoring (1-2 years)
3. Team Leadership (2-3 years)
4. Strategic Planning (ongoing)

### Path 3: QA Career Track (1-3 years)
1. CS Fundamentals
2. Testing Frameworks
3. Test Automation
4. Performance Testing
5. QA Architecture

### Path 4: DevRel/Technical Writing (2-4 years)
1. Strong Communication
2. Technical Content Creation
3. Community Building
4. Advocacy & Speaking
5. Product Strategy

## Salary Ranges

| Role | Salary | Timeline | Demand |
|------|--------|----------|--------|
| Senior Software Engineer | $150K-300K+ | 5-10 yrs | High |
| Engineering Manager | $130K-400K+ | 5-15 yrs | High |
| Staff Engineer | $160K-320K+ | 8-12 yrs | High |
| DevRel Engineer | $80K-200K+ | 3-5 yrs | Growing |
| QA Architect | $90K-210K+ | 5-10 yrs | Stable |
| Technical Writer | $50K-150K+ | 2-5 yrs | Growing |
| Rust Systems Dev | $120K-250K+ | 2-3 yrs | Very High |

## Project Examples

1. **Sorting Algorithm Implementation** - Compare algorithms
2. **Graph Traversal Problems** - DFS, BFS, shortest path
3. **LeetCode Problems** - Practice algorithmic thinking
4. **Git Workflow Mastery** - Team collaboration scenario
5. **Rust Systems Tool** - CLI application, WebAssembly
6. **C++ Game Engine** - Performance-critical code
7. **Technical Documentation** - API docs, guides

## Algorithm Interview Prep

```python
# Example: LeetCode Problem - Two Sum
def twoSum(nums: list[int], target: int) -> list[int]:
    seen = {}
    for i, num in enumerate(nums):
        complement = target - num
        if complement in seen:
            return [seen[complement], i]
        seen[num] = i
    return []

# Time: O(n), Space: O(n)
```

## When to Use This Skill

- Algorithm interviews
- System design interviews
- Choosing programming languages
- Building performance-critical code
- Career planning
- Technical mentoring
- Engineering management transition
- Open-source contribution
- Teaching programming

## Related Agents

All agents benefit from strong fundamentals:
- **Backend Agent** - Algorithms for optimization
- **Frontend Agent** - Performance algorithms
- **Infrastructure Agent** - System design concepts
- **Data Science Agent** - Algorithm complexity
- **Database Agent** - Data structure selection

## Resources

**Books:**
- *Introduction to Algorithms* (CLRS) - Gold standard
- *Algorithm Design Manual* (Skiena)
- *Cracking the Coding Interview* (Paxson McDowell)
- *C++ Primer* (Lippman et al.)
- *The Rust Programming Language*

**Online Platforms:**
- LeetCode (800+ problems)
- HackerRank (practice)
- CodeSignal (interviews)
- InterviewBit (prep)
- ProjectEuler (math problems)

**Courses:**
- MIT OpenCourseWare (CS fundamentals)
- Stanford (CS education)
- Coursera (algorithms)
- Frontend Masters (system design)

**Git Resources:**
- Pro Git Book (Chacon & Straub) - FREE
- GitHub Learning Lab
- Atlassian Git Tutorials
- Oh Shit, Git!?

---

**Status:** Comprehensive fundamentals skill covering 9 roles and 1,200+ topics

**Estimated Learning Time:**
- CS + DSA + Git: 6-12 months (part-time)
- Add Rust/C++: 12-24 months additional
- Career development: Ongoing throughout career
