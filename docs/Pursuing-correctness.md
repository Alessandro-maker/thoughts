# Pursuing correctness

## Principles

1) Correctness and security are two different things. Here I write about correctness.
2) Demostrations over tests
3) No effect over local effect over wider effect
4) Tests over nothing
5) Error states and code bugs are two different things. Both need to be properly detected and managed. Differently.
6) Beware code dependent from execution time (ex.: _new Date()_, _NOW()_, etc.). It opens the door to race conditions and not repetable tests.
7) Balance costs (induced architectural limitations, development, maintenance over code changes, sinked complexity as technical debt) and gains (cleaner architecture and code redability, coded knowledge, less worries for unforesight effects while coding and for different code areas and documentation going out of sync, having your back guarded during refactories, easier collaboration, lower onboarding, more local reasoning). State project tradeoffs as soon as possible.

## Guidelines

- Stricly type input and output for any non-trivial chunk of code. Let type inference for trivial ones.
- Don't use _any_. When you have to use it properly mark it, take extra care, surround with assertions and check with tests.
- Use always _unknown_ for external inputs. Prefer parsers (function that convert a less typed data structure to a more stricly typed one) over validators (function that verify check input but let it unchanged).
- Use type casts for compiler or unavoidable architectural limitations only. When you have to use it properly mark it, take extra care, surround with assertions and check with tests.
- Use of parsers over validators usually let you avoid to cast over conditions you already checked and that compiler can't infer.
- Use proper assetions []
- Test must be fully repetable.
- If you have to rely on execution time (ex: time-expired condition) use a common time for the request or transition. Use for example request start time. When testing this time must be supplied as input test data so part of saved test data or generated from seed for fuztests. This way tests can be repetable.
