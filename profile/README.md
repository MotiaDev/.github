<p align="center">
  <!-- shows in LIGHT mode only -->
  <img src="https://github.com/MotiaDev/motia/raw/main/assets/motia-logo-light.png#gh-dark-mode-only"  width="400" alt="Motia logo" />
  <!-- shows in DARK mode only -->
  <img src="https://github.com/MotiaDev/motia/raw/main/assets/motia-logo-dark.png#gh-light-mode-only" width="400" alt="Motia logo (dark)" />
</p>

<div align="center">

🔥 A Modern Unified Backend Framework for APIs, Events, and Agents 🔥

[![Website](https://img.shields.io/badge/Website-motia.dev-blue?style=flat&logo=globe&logoColor=white&labelColor=000000)](https://www.motia.dev)
[![Documentation](https://img.shields.io/badge/Docs-motia.dev-green?style=flat&logo=gitbook&logoColor=white&labelColor=000000)](https://www.motia.dev/docs)
[![npm](https://img.shields.io/npm/v/motia?style=flat&logo=npm&logoColor=white&color=CB3837&labelColor=000000)](https://www.npmjs.com/package/motia)
[![License](https://img.shields.io/badge/license-MIT-green?style=flat&logo=opensourceinitiative&logoColor=white&labelColor=000000)](LICENSE)

[![GitHub Stars](https://img.shields.io/github/stars/MotiaDev/motia?style=flat&logo=github&logoColor=white&color=yellow&labelColor=000000)](https://github.com/MotiaDev/motia)
[![Discord](https://img.shields.io/discord/1322278831184281721?style=flat&logo=discord&logoColor=white&color=5865F2&label=Discord&labelColor=000000)](https://discord.gg/motia)
[![Twitter Follow](https://img.shields.io/badge/Follow-@motiadev-1DA1F2?style=flat&logo=twitter&logoColor=white&labelColor=000000)](https://twitter.com/motiadev)

---

</div>

## 🎯 What is Motia?

Backend development today is fragmented.

APIs live in one framework, background jobs in another, queues and schedulers elsewhere, and now AI agents and streaming systems have their own runtimes. Add observability and state management on top, and you're stitching together half a dozen tools before writing your first feature.

**Motia unifies all of these concerns around one core primitive: the Step.**

Just as React made frontend development simple by introducing components, Motia redefines backend development with Steps.

Every backend pattern, API endpoints, background jobs, queues, workflows, AI agents, streaming, observability, and state, is expressed with the same primitive.

To read more about this, check out our **[manifesto](https://motia.dev/manifesto)**.

---

## The Core Primitive: the Step

A Step is just a file with a `config` and a `handler`. Motia auto-discovers these files and connects them automatically.

Here's a simple example of two Steps working together: an API Step that emits an event, and an Event Step that processes it.

<details open>
<summary><b>TypeScript</b></summary>

```ts
// steps/send-message.step.ts
export const config = {
  name: 'SendMessage',
  type: 'api',
  path: '/messages',
  method: 'POST',
  emits: ['message.sent']
};

export const handler = async (req, { emit }) => {
  await emit({
    topic: 'message.sent',
    data: { text: req.body.text }
  });
  return { status: 200, body: { ok: true } };
};
```

```ts
// steps/process-message.step.ts
export const config = {
  name: 'ProcessMessage',
  type: 'event',
  subscribes: ['message.sent']
};

export const handler = async (input, { logger }) => {
  logger.info('Processing message', input);
};
```

</details>

<details close>
<summary><b>Python</b></summary>

```python
# send_message_step.py
config = {
    "name": "SendMessage",
    "type": "api",
    "path": "/messages",
    "method": "POST",
    "emits": ["message.sent"]
}

async def handler(req, context):
    await context.emit({
        "topic": "message.sent",
        "data": {"text": req.body["text"]}
    })
    return {"status": 200, "body": {"ok": True}}
```

```python
# process_message_step.py
config = {
    "name": "ProcessMessage",
    "type": "event",
    "subscribes": ["message.sent"]
}

async def handler(input, context):
    context.logger.info("Processing message", input)
```

</details close>

<details>
<summary><b>JavaScript</b></summary>

```js
// steps/send-message.step.js
const config = {
  name: 'SendMessage',
  type: 'api',
  path: '/messages',
  method: 'POST',
  emits: ['message.sent']
};

const handler = async (req, { emit }) => {
  await emit({
    topic: 'message.sent',
    data: { text: req.body.text }
  });
  return { status: 200, body: { ok: true } };
};

module.exports = { config, handler };
```

```js
// steps/process-message.step.js
const config = {
  name: 'ProcessMessage',
  type: 'event',
  subscribes: ['message.sent']
};

const handler = async (input, { logger }) => {
  logger.info('Processing message', input);
};

module.exports = { config, handler };
```

</details>

👉 With just two files, you've built an **API endpoint**, a **queue**, and a **worker**. No extra frameworks required.

**[Learn more about Steps →](https://motia.dev/docs/concepts/steps/steps)**


Read [our documentation](https://www.motia.dev/docs) and get started today: `npx motia@latest create`

![GitHub commit activity](https://img.shields.io/github/commit-activity/m/MotiaDev/motia?style=flat&logo=github&logoColor=white&labelColor=000000)
![GitHub issues](https://img.shields.io/github/issues/MotiaDev/motia?style=flat&logo=github&logoColor=white&labelColor=000000)
![GitHub pull requests](https://img.shields.io/github/issues-pr/MotiaDev/motia?style=flat&logo=github&logoColor=white&labelColor=000000)

**Join thousands of developers building the future of backend development**

</div>

## 🤝 Contributing

We love contributions! Check out our [Contributing Guide](CONTRIBUTING.md) to get started.

<div align="center">

[![Contributors](https://contrib.rocks/image?repo=MotiaDev/motia)](https://github.com/MotiaDev/motia/graphs/contributors)

</div>

## 📄 License

Motia is [MIT licensed](LICENSE) and open source. Build amazing things! 🚀

---

<div align="center">

**[Website](https://www.motia.dev)** • **[Documentation](https://www.motia.dev/docs)** • **[Discord](https://discord.gg/EnfDRFYW)** • **[Twitter](https://twitter.com/motiadev)**

Made with ❤️ by the Motia team and community

</div>
