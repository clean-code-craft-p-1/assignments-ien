# Naming as a way to guide modularity

If you use "clear" names, developers can understand the code quickly - aiding in productivity.
If not, they need to lookup the context _many times_ when they encounter it in the code.

Example: function doing input-validation of temperature

>The naming consideration is: How does this function look in the other functions that call it? Do we need to see its implementation to understand the calling code?

Candidate names for illustration:

| Name | Comment | How it looks in the caller |
|---|---|---|
| `checkMinMax` | Reflects the implementation | What's the purpose? What does it do if it's not in range? |
| `inputValidation` | Generic statement of functionality | What validation does it do? What happens when validation fails? |
| `temperatureCheck` | Captures the domain (temperature) | What happens if the check passes or fails? |
| `isValidHumanTemperature` | (self-evident) | Clear, boolean result. Not expected to change state. What's the unit of the input? |

## The tension of naming

Sometimes, a tension in naming can reveal opportunities for single-responsibility, encapsulation, or issues like duplication.

In [this folder having reporters](https://github.com/clean-code-craft-p-1/clean-code-craft-p-1-modularity-in-cs-modularity-cs/tree/10ad9b6a1843bc8e2fc4c78d8d6bc82eaa7d26be/Reporting), the file [FileReportGenerator.cs](https://github.com/clean-code-craft-p-1/clean-code-craft-p-1-modularity-in-cs-modularity-cs/blob/10ad9b6a1843bc8e2fc4c78d8d6bc82eaa7d26be/Reporting/FileReportGenerator.cs) calls the [console-writer](https://github.com/clean-code-craft-p-1/clean-code-craft-p-1-modularity-in-cs-modularity-cs/blob/10ad9b6a1843bc8e2fc4c78d8d6bc82eaa7d26be/Reporting/ConsoleReportWriter.cs) as well as the [file-writer](https://github.com/clean-code-craft-p-1/clean-code-craft-p-1-modularity-in-cs-modularity-cs/blob/10ad9b6a1843bc8e2fc4c78d8d6bc82eaa7d26be/Reporting/FileReportWriter.cs)

But the name `FileReportGenerator` doesn't convery that. Perhaps the tension has to do with the fact that "writing to both console and file" is not a requirement in the domain. If it is, maybe the requirement would be worded as "write report in multiple formats", in which case the name can be `MultimodalReportGenerator`

## Idea

Can static analysis nudge us to use better names in the IDE itself?

Choices:
- Spell check plugin: VSCode and most IDEs have this, which is sensitive to Pascal/snake/camelCase. They give the 'red underline' on spelling issues
- Manually mark a section of code and ask the LLM (copilot) to review. It will highlight the issues, excluding legacy code in the same file.  
- Automatic naming suggestion - Are there any tools for this?
