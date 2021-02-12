# Pursuing correctness

## Principles

1. Correctness and security are two different things. Here I write about correctness.
2. Error states and code bugs are two different things (See [https://blog.regehr.org/archives/1091]). Both need to be properly detected and managed. Differently.
3. Demonstrations over tests
4. No effect over local effect over wider effect
5. Tests over nothing
6. Documentation is usually your last defence line (in addition to helping future you and others a lot). Don't disregard it and make it effective.
7. Beware code dependent from execution time (ex.: _new Date()_, _NOW()_, etc.). It opens the door to race conditions and not repeatable tests.
8. Balance costs (induced architectural limitations, development, maintenance over code changes, sunk complexity as technical debt) and gains (cleaner architecture and code readability, coded knowledge, less worries for unforesight effects while coding and for different code areas and documentation going out of sync, having your back guarded during refactories, easier collaboration, lower onboarding, more local reasoning). State project tradeoffs as soon as possible.

## Guidelines

- Strictly type input and output for any non-trivial chunk of code. Let type inference for trivial ones.
- Don't use _any_. When you have to use it mark it properly, take extra care, surround with assertions and check with tests.
- Use always _unknown_ for external inputs. Prefer parsers (function that convert a less typed data structure to a more strictly typed one) over validators (function that check input but let it unchanged).
- Use type casts for compiler limitations or unavoidable architectural limitations only. When you have to use it mark it properly, take extra care, surround with assertions and check with tests.
- Use of parsers over validators usually let you avoid to cast over conditions you already checked and that compiler can't infer.
- Use proper assertions
- Test must be fully repeatable.
- If you have to rely on execution time (ex: time-expired condition) use a common time for the request or transition. Use for example request start time. When testing this time must be supplied as input test data so part of saved test data or generated from seed for fuztests. This way tests can be repeatable.
- Don't hurry for code abstraction and extraction. Usually wait for a bunch of use cases.
- Keep together (near) code that usually change together
- Keep documentation as near as possible to code it refers
- Document _why_ and remember to document _why not_ (failed experiments, if not documented, tends to repeat themself. same as history)
- Document _what_ only if code clarity sucks and there's nothing you can do about it. Document why it can't suck less and failed experiments too.
