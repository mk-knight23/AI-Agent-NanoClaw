# Swarm Orchestration — NanoClaw

NanoClaw acts as the orchestrator in a multi-agent swarm, spawning and coordinating worker agents for tasks that benefit from parallelism.

## Trigger
- **Manual**: `@NanoClaw swarm "<goal>"`
- **API**: `POST /swarm` with `{ "goal": "...", "max_agents": 5 }`

## Architecture

```
User → NanoClaw (Orchestrator)
           ├── Worker 1: Subtask A
           ├── Worker 2: Subtask B
           ├── Worker 3: Subtask C
           └── Synthesize → Response
```

## Supported Swarm Patterns

### Parallel Research
```
@NanoClaw swarm "compare Supabase, PlanetScale, and Neon for our use case"
```
Spawns 3 workers in parallel, orchestrator synthesizes a comparison table.

### Map-Reduce
```
@NanoClaw swarm "audit all 30 repos in our org for outdated dependencies"
```
Maps across repos simultaneously, reduces to a priority list.

### Pipeline
```
@NanoClaw swarm "for each item in todo.txt: research, draft solution, test"
```
Sequential pipeline with parallelism within each stage.

## Configuration

```typescript
// config/swarm.ts
export const swarmConfig = {
  maxAgents: 5,
  agentModel: 'haiku',         // Cost-efficient for workers
  orchestratorModel: 'sonnet', // Full model for coordination
  timeoutSeconds: 300,
  retryOnFailure: true,
};
```

## Worker Communication

Workers share state via an in-memory message queue (or Supabase if `add-supabase` is installed). The orchestrator polls for results and reassigns failed tasks.
