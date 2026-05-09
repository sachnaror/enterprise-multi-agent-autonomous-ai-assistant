
```
ai_assistant/
│
├── app/
│   │
│   ├── main.py                                  # FastAPI application entrypoint
│   ├── config.py                                # Centralized configuration management
│   ├── models.py                                # Shared schemas and dataclasses
│   ├── dependencies.py                          # Dependency injection helpers
│   ├── constants.py                             # Shared constants and enums
│   ├── logging_config.py                        # Structured logging configuration
│   │
│   ├── api/
│   │   ├── routes.py                            # Registers all application routes
│   │   ├── chat_routes.py                       # Chat and conversation APIs
│   │   ├── memory_routes.py                     # Memory-system APIs
│   │   ├── agent_routes.py                      # Agent execution APIs
│   │   ├── indexing_routes.py                   # RAG/indexing APIs
│   │   ├── workflow_routes.py                   # Workflow and DAG execution APIs
│   │   ├── approval_routes.py                   # Human approval APIs
│   │   ├── observability_routes.py              # Metrics/tracing APIs
│   │   └── health_routes.py                     # Health and readiness endpoints
│   │
│   ├── prompts/
│   │   ├── system_prompt.md                     # Master AI assistant system prompt
│   │   ├── planner_prompt.md                    # Planner-agent prompt template
│   │   ├── coder_prompt.md                      # Coding-agent prompt template
│   │   ├── validator_prompt.md                  # Validation-agent prompt template
│   │   ├── rag_prompt.md                        # Retrieval prompt template
│   │   ├── summarizer_prompt.md                 # Conversation summarization prompt
│   │   ├── memory_prompt.md                     # Long-context memory optimization prompt
│   │   ├── reflection_prompt.md                 # Self-reflection and critique prompt
│   │   ├── reviewer_prompt.md                   # Code-review and validation prompt
│   │   └── planning_prompt.md                   # DAG planning and execution prompt
│   │
│   ├── agents/
│   │   ├── orchestrator.py                      # Routes tasks across specialized agents
│   │   ├── planner_agent.py                     # Creates execution plans
│   │   ├── rag_agent.py                         # Handles retrieval-augmented reasoning
│   │   ├── validator_agent.py                   # Validates outputs and architecture
│   │   ├── graph_agent.py                       # Handles graph-based reasoning
│   │   ├── coder_agent.py                       # Generates and edits code
│   │   ├── reviewer_agent.py                    # Reviews generated code changes
│   │   ├── debugging_agent.py                   # Investigates runtime issues
│   │   ├── memory_agent.py                      # Coordinates memory lifecycle
│   │   ├── retrieval_agent.py                   # Retrieves semantic context
│   │   ├── deployment_agent.py                  # Handles infra/deployment reasoning
│   │   ├── reflection_agent.py                  # Performs self-critique and correction
│   │   ├── evaluation_agent.py                  # Scores and evaluates generated outputs
│   │   ├── execution_agent.py                   # Executes DAG tasks safely
│   │   ├── checkpoint_agent.py                  # Handles checkpoint recovery/resume
│   │   ├── coordination_agent.py                # Coordinates multi-agent communication
│   │   └── tool_selector_agent.py               # Dynamically selects tools
│   │
│   ├── memory/
│   │   ├── session_manager.py                   # Handles user-session lifecycle
│   │   ├── session_store.py                     # Redis-backed short-term sessions
│   │   ├── memory_router.py                     # Routes memory across storage layers
│   │   ├── context_builder.py                   # Builds optimized LLM context
│   │   ├── context_optimizer.py                 # Optimizes final context payload
│   │   ├── compression.py                       # Compresses long conversations
│   │   ├── summarizer.py                        # Summarizes historical conversations
│   │   ├── retrieval_pipeline.py                # Multi-stage memory retrieval pipeline
│   │   ├── retrieval_ranker.py                  # Reranks retrieved memory chunks
│   │   ├── token_budget_manager.py              # Controls token/context limits
│   │   ├── importance_scorer.py                 # Scores memory importance
│   │   ├── semantic_cache.py                    # Caches semantic retrieval results
│   │   ├── memory_indexer.py                    # Indexes memories into vector DB
│   │   ├── memory_models.py                     # Shared memory schemas
│   │   ├── memory_cleaner.py                    # Cleans expired/low-value memories
│   │   ├── memory_scheduler.py                  # Schedules summarization/archive jobs
│   │   ├── embedding_service.py                 # Embedding-generation service
│   │   ├── memory_metrics.py                    # Tracks memory-system metrics
│   │   ├── memory_audit.py                      # Audits memory retrieval/access
│   │   └── memory_constants.py                  # Shared memory constants
│   │
│   │   ├── episodic/                            # Historical conversation memory
│   │   ├── semantic/                            # Semantic fact-based memory
│   │   ├── procedural/                          # Workflow and execution-pattern memory
│   │   ├── working/                             # Active short-term working memory
│   │   ├── archival/                            # Archived long-term conversations
│   │   ├── rehydration/                         # Context/session restoration logic
│   │   ├── policies/                            # Retention and expiration policies
│   │   ├── compression/                         # Semantic compression utilities
│   │   ├── pipelines/                           # Memory ingestion/retrieval pipelines
│   │   ├── strategies/                          # Retrieval/ranking strategies
│   │   ├── providers/                           # Redis/Postgres/S3 providers
│   │   ├── jobs/                                # Scheduled background memory jobs
│   │   └── experiments/                         # Long-context experimentation
│   │
│   ├── tools/
│   │   ├── registry.py                          # Central tool registry
│   │   ├── tool_executor.py                     # Executes tools securely
│   │   ├── tool_definitions.py                  # Shared TOOLS registry definition
│   │   ├── file_tools.py                        # Filesystem read/write tools
│   │   ├── terminal_tools.py                    # Terminal-command execution tools
│   │   ├── search_tools.py                      # Grep/glob/semantic search tools
│   │   ├── git_tools.py                         # Git interaction tools
│   │   ├── browser_tools.py                     # URL/browser interaction tools
│   │   ├── diff_tools.py                        # Diff generation and validation
│   │   ├── indexing_tools.py                    # Indexing-related utility tools
│   │   ├── mcp_tools.py                         # MCP-based external tools
│   │   ├── sandbox_tools.py                     # Sandboxed execution helpers
│   │   ├── filesystem_guard.py                  # Prevents unsafe filesystem access
│   │   ├── network_guard.py                     # Restricts unsafe network access
│   │   ├── safe_terminal.py                     # Restricted terminal execution
│   │   └── execution_monitor.py                 # Monitors tool execution safety
│   │
│   ├── indexing/
│   │   ├── code_indexer.py                      # Source-code indexing engine
│   │   ├── incremental_indexer.py               # Re-indexes changed files only
│   │   ├── file_watcher.py                      # Watches project filesystem changes
│   │   ├── hash_tracker.py                      # Tracks file hashes for change detection
│   │   ├── git_diff_analyzer.py                 # Uses git diff for incremental indexing
│   │   ├── semantic_diff.py                     # Detects meaningful semantic code changes
│   │   ├── dependency_tracker.py                # Tracks dependency-impact graph
│   │   ├── stale_index_cleaner.py               # Removes obsolete embeddings/chunks
│   │   ├── change_detector.py                   # Detects impactful file changes
│   │   ├── symbol_graph.py                      # Builds dependency/symbol graph
│   │   ├── embeddings_cache.py                  # Cached embeddings storage
│   │   ├── ast_parser.py                        # AST-based source parser
│   │   ├── dependency_mapper.py                 # Maps imports and dependencies
│   │   ├── semantic_map.py                      # Semantic codebase graph
│   │   ├── repository_graph.py                  # Repository-wide dependency graph
│   │   ├── mmap_search.py                       # Memory-mapped ultra-fast file search
│   │   ├── ripgrep_wrapper.py                   # High-speed ripgrep integration
│   │   ├── bm25_indexer.py                      # BM25 keyword indexing engine
│   │   ├── hybrid_indexer.py                    # Hybrid semantic + keyword indexing
│   │   ├── chunk_manager.py                     # Intelligent code/document chunking
│   │   ├── treesitter_parser.py                 # Tree-sitter parser integration
│   │   ├── symbol_extractor.py                  # Extracts functions/classes/imports
│   │   ├── code_navigation.py                   # Fast code navigation engine
│   │   └── repo_analyzer.py                     # Repository-analysis orchestration
│   │
│   ├── search/
│   │   ├── ast_indexer.py                       # AST-aware indexing engine
│   │   ├── symbol_indexer.py                    # Symbol-based code indexing
│   │   ├── import_graph.py                      # Import/dependency graph builder
│   │   ├── semantic_search.py                   # Semantic retrieval search
│   │   ├── bm25_search.py                       # BM25 keyword-based retrieval
│   │   ├── hybrid_search.py                     # Hybrid semantic + keyword search
│   │   ├── mmap_search.py                       # Ultra-fast memory-mapped search
│   │   ├── ripgrep_wrapper.py                   # ripgrep integration for fast search
│   │   ├── code_navigation.py                   # Intelligent repository navigation
│   │   └── repository_graph.py                  # Repository knowledge graph
│   │
│   ├── parsers/
│   │   ├── treesitter_parser.py                 # Tree-sitter parsing engine
│   │   ├── python_parser.py                     # Python AST/syntax parser
│   │   ├── js_parser.py                         # JavaScript parser
│   │   ├── ts_parser.py                         # TypeScript parser
│   │   ├── symbol_extractor.py                  # Extracts repository symbols
│   │   ├── ast_chunker.py                       # AST-aware chunking logic
│   │   └── semantic_chunker.py                  # Semantic-aware chunk generation
│   │
│   ├── planning/
│   │   ├── dag_builder.py                       # Builds DAG-based execution plans
│   │   ├── dependency_resolver.py               # Resolves workflow dependencies
│   │   ├── task_graph.py                        # Multi-step task graph engine
│   │   ├── execution_planner.py                 # Parallel execution planner
│   │   ├── retry_planner.py                     # Handles retry/recovery planning
│   │   ├── task_scheduler.py                    # Schedules parallel workflows
│   │   └── workflow_optimizer.py                # Optimizes workflow execution order
│   │
│   ├── state/
│   │   ├── agent_state.py                       # Tracks agent lifecycle state
│   │   ├── workflow_state.py                    # Tracks workflow execution state
│   │   ├── task_state.py                        # Tracks task-level state
│   │   ├── execution_state.py                   # Tracks runtime execution state
│   │   ├── checkpoint_manager.py                # Saves workflow checkpoints
│   │   ├── state_persistence.py                 # Persists workflow/agent state
│   │   └── recovery_state.py                    # Handles recovery/resume state
│   │
│   ├── checkpoints/
│   │   ├── checkpoint_store.py                  # Stores workflow snapshots
│   │   ├── workflow_snapshot.py                 # Workflow checkpoint snapshots
│   │   ├── recovery_manager.py                  # Restores failed workflows
│   │   ├── replay_engine.py                     # Replays interrupted execution
│   │   ├── rollback_manager.py                  # Rolls back failed actions safely
│   │   └── execution_history.py                 # Stores execution history timeline
│   │
│   ├── sandbox/
│   │   ├── docker_runner.py                     # Docker-isolated code execution
│   │   ├── vm_runner.py                         # VM-based isolated execution
│   │   ├── restricted_shell.py                  # Restricted shell execution layer
│   │   ├── policy_enforcer.py                   # Enforces sandbox security policies
│   │   ├── filesystem_guard.py                  # Restricts filesystem access
│   │   ├── network_guard.py                     # Restricts external network calls
│   │   ├── execution_monitor.py                 # Monitors runtime safety
│   │   └── resource_limiter.py                  # CPU/RAM/process usage limiting
│   │
│   ├── events/
│   │   ├── event_bus.py                         # Central async event bus
│   │   ├── event_models.py                      # Event payload schemas
│   │   ├── websocket_streamer.py                # WebSocket event streaming
│   │   ├── sse_streamer.py                      # SSE-based realtime streaming
│   │   ├── task_updates.py                      # Live task progress updates
│   │   ├── agent_events.py                      # Agent lifecycle events
│   │   ├── observability_events.py              # Metrics/tracing events
│   │   └── notification_dispatcher.py           # Notification/event dispatcher
│   │
│   ├── coordination/
│   │   ├── message_bus.py                       # Multi-agent communication bus
│   │   ├── shared_blackboard.py                 # Shared reasoning context
│   │   ├── task_queue.py                        # Distributed task queue
│   │   ├── agent_registry.py                    # Tracks active agents
│   │   ├── collaboration_manager.py             # Coordinates agent collaboration
│   │   └── delegation_manager.py                # Handles task delegation
│   │
│   ├── approval/
│   │   ├── diff_reviewer.py                     # Reviews generated diffs
│   │   ├── approval_queue.py                    # Human approval workflow queue
│   │   ├── human_gate.py                        # Requires human intervention when risky
│   │   ├── risk_assessor.py                     # Scores execution risk
│   │   ├── safe_execution.py                    # Executes only approved actions
│   │   └── approval_policies.py                 # Defines approval policies
│   │
│   ├── observability/
│   │   ├── tracing.py                           # OpenTelemetry tracing integration
│   │   ├── metrics.py                           # Prometheus/Grafana metrics
│   │   ├── token_tracking.py                    # Tracks token consumption
│   │   ├── agent_logs.py                        # Structured agent logs
│   │   ├── prompt_logs.py                       # Prompt execution logs
│   │   ├── memory_metrics.py                    # Memory-system metrics
│   │   ├── latency_tracker.py                   # Measures execution latency
│   │   ├── hallucination_tracker.py             # Tracks hallucination patterns
│   │   ├── audit_trail.py                       # Enterprise audit logging
│   │   └── execution_dashboard.py               # Aggregates observability dashboards
│   │
│   ├── evaluation/
│   │   ├── benchmark_runner.py                  # Runs benchmark evaluations
│   │   ├── prompt_eval.py                       # Evaluates prompt quality
│   │   ├── retrieval_eval.py                    # Evaluates retrieval quality
│   │   ├── hallucination_eval.py                # Measures hallucination rate
│   │   ├── agent_scorecard.py                   # Scores agent performance
│   │   ├── regression_tests.py                  # Prevents behavioral regressions
│   │   ├── memory_eval.py                       # Evaluates memory quality
│   │   └── execution_eval.py                    # Evaluates execution correctness
│   │
│   ├── reflection/
│   │   ├── self_critique.py                     # Self-reflection reasoning loop
│   │   ├── reasoning_validator.py               # Validates reasoning quality
│   │   ├── correction_loop.py                   # Attempts self-correction
│   │   ├── confidence_scorer.py                 # Calculates response confidence
│   │   ├── hallucination_guard.py               # Detects hallucinated reasoning
│   │   └── response_refiner.py                  # Refines low-confidence outputs
│   │
│   ├── governance/
│   │   ├── token_governor.py                    # Controls token usage budgets
│   │   ├── model_router.py                      # Routes requests to best-fit model
│   │   ├── budget_limits.py                     # Defines provider spending limits
│   │   ├── provider_fallback.py                 # Handles provider/model fallback
│   │   ├── rate_limiter.py                      # Controls API/request rate limits
│   │   ├── quota_manager.py                     # Manages user/team quotas
│   │   └── policy_engine.py                     # Enforces governance policies
│   │
│   ├── graph/
│   │   ├── neo4j_client.py                      # Neo4j graph database integration
│   │   ├── entity_extractor.py                  # Extracts graph entities
│   │   ├── relationship_mapper.py               # Builds graph relationships
│   │   ├── graph_search.py                      # Graph-based semantic traversal
│   │   ├── repository_knowledge_graph.py        # Repository-level knowledge graph
│   │   ├── dependency_graph.py                  # Code dependency graph
│   │   └── architecture_graph.py                # System architecture relationship graph
│   │
│   ├── skills/
│   │   ├── python_skill.md                      # Python engineering operational skill
│   │   ├── fastapi_skill.md                     # FastAPI engineering operational skill
│   │   ├── kubernetes_skill.md                  # Kubernetes operational skill
│   │   ├── postgres_skill.md                    # PostgreSQL operational skill
│   │   ├── debugging_skill.md                   # Debugging and troubleshooting skill
│   │   ├── rag_skill.md                         # RAG-engineering operational skill
│   │   ├── async_skill.md                       # Async/concurrency engineering skill
│   │   └── security_skill.md                    # Security engineering operational skill
│   │
│   └── ...
│
├── storage/                                     # Persistent storage layer
├── infrastructure/                              # Infra and deployment configuration
├── knowledge/                                   # Long-term organizational knowledge
├── tests/                                       # Automated tests and evaluations
├── scripts/                                     # DevOps and operational scripts
├── .claude/                                     # Claude-specific commands/rules
├── .codex/                                      # Codex-specific commands/rules
├── CLAUDE.md                                    # Claude operating instructions
├── AGENTS.md                                    # Multi-agent orchestration guide
├── SKILLS.md                                    # Shared engineering skills memory
├── README.md                                    # Project overview and setup guide
├── docker-compose.yml                           # Multi-service orchestration
├── pyproject.toml                               # Python tooling/dependency config
├── requirements.txt                             # Python dependencies
└── Makefile                                     # Developer automation commands
```
