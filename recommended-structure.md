This is a scalable reference architecture, not something every project must fully implement. Choose only the modules relevant to your application's size, complexity, and use case, and expand incrementally as requirements grow.

Understand what each folder, layer, and system actually does before adding it, and do not blindly follow this structure unless there is a real architectural need for it.



```text
ai_assistant/
│
├── app/
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
│   │   ├── compression_manager.py               # Central compression orchestration layer
│   │   ├── summarizer.py                        # Summarizes historical conversations
│   │   ├── retrieval_orchestrator.py            # Coordinates memory retrieval pipeline
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
│   │   ├── memory_constants.py                  # Shared memory constants
│   │   │
│   │   ├── episodic/
│   │   │   ├── episodic_store.py                # Stores historical conversations
│   │   │   ├── episodic_retriever.py            # Retrieves related conversations
│   │   │   ├── episodic_summarizer.py           # Summarizes old chat sessions
│   │   │   ├── episodic_models.py               # Episodic-memory schemas
│   │   │   └── episodic_ranker.py               # Ranks historical memory relevance
│   │   │
│   │   ├── semantic/
│   │   │   ├── semantic_store.py                # Stores semantic memories
│   │   │   ├── semantic_retriever.py            # Retrieves semantic context
│   │   │   ├── semantic_extractor.py            # Extracts facts/preferences
│   │   │   ├── semantic_embeddings.py           # Embedding management
│   │   │   ├── semantic_models.py               # Semantic-memory schemas
│   │   │   └── semantic_ranker.py               # Semantic retrieval ranking
│   │   │
│   │   ├── procedural/
│   │   │   ├── procedural_store.py              # Stores workflows/procedures
│   │   │   ├── procedural_retriever.py          # Retrieves reusable workflows
│   │   │   ├── workflow_memory.py               # Learns execution patterns
│   │   │   ├── procedural_models.py             # Procedural-memory schemas
│   │   │   └── workflow_optimizer.py            # Optimizes reusable workflows
│   │   │
│   │   ├── working/
│   │   │   ├── working_memory.py                # Active runtime memory
│   │   │   ├── conversation_window.py           # Rolling recent context
│   │   │   ├── active_task_store.py             # Current unfinished tasks
│   │   │   ├── temporary_context.py             # Runtime temporary context
│   │   │   ├── working_models.py                # Working-memory schemas
│   │   │   └── context_pruner.py                # Removes low-priority context
│   │   │
│   │   ├── archival/
│   │   │   ├── archive_manager.py               # Handles archival lifecycle
│   │   │   ├── s3_archiver.py                   # Uploads archives to S3
│   │   │   ├── archive_retriever.py             # Retrieves archived memory
│   │   │   ├── archive_compressor.py            # Compresses archives
│   │   │   ├── archival_models.py               # Archive schemas
│   │   │   └── cold_storage_cleaner.py          # Cleans stale archives
│   │   │
│   │   ├── rehydration/
│   │   │   ├── session_rehydrator.py            # Restores prior sessions
│   │   │   ├── context_restorer.py              # Restores optimized context
│   │   │   ├── semantic_bootstrap.py            # Loads semantic memory
│   │   │   ├── active_task_restorer.py          # Restores unfinished tasks
│   │   │   └── memory_bootstrapper.py           # Initializes memory state
│   │   │
│   │   ├── policies/
│   │   │   ├── retention_policy.py              # Memory-retention rules
│   │   │   ├── expiration_policy.py             # Expiration/TTL logic
│   │   │   ├── archival_policy.py               # Archive decision rules
│   │   │   ├── cleanup_policy.py                # Cleanup rules
│   │   │   ├── importance_policy.py             # Importance scoring policies
│   │   │   └── storage_policy.py                # Storage routing policies
│   │   │
│   │   ├── compression/
│   │   │   ├── semantic_compressor.py           # Semantic memory compression
│   │   │   ├── deduplicator.py                  # Removes duplicate memories
│   │   │   ├── embedding_optimizer.py           # Optimizes embeddings
│   │   │   ├── chunk_compressor.py              # Compresses oversized chunks
│   │   │   ├── token_reducer.py                 # Reduces token usage
│   │   │   └── summary_compactor.py             # Compacts long summaries
│   │   │
│   │   ├── pipelines/
│   │   │   ├── ingestion_pipeline.py            # Memory ingestion flow
│   │   │   ├── summarization_pipeline.py        # Summarization workflow
│   │   │   ├── compression_pipeline.py          # Compression orchestration
│   │   │   ├── retrieval_pipeline.py            # Retrieval orchestration
│   │   │   ├── embedding_pipeline.py            # Embedding workflow
│   │   │   ├── archival_pipeline.py             # Archival workflow
│   │   │   └── rehydration_pipeline.py          # Session restore pipeline
│   │   │
│   │   ├── strategies/
│   │   │   ├── recency_strategy.py              # Recent-context prioritization
│   │   │   ├── relevance_strategy.py            # Relevance ranking logic
│   │   │   ├── importance_strategy.py           # Importance-aware retrieval
│   │   │   ├── token_strategy.py                # Token optimization strategy
│   │   │   ├── hybrid_strategy.py               # Hybrid retrieval logic
│   │   │   └── decay_strategy.py                # Memory-decay logic
│   │   │
│   │   ├── providers/
│   │   │   ├── redis_provider.py                # Redis integration
│   │   │   ├── postgres_provider.py             # PostgreSQL integration
│   │   │   ├── pgvector_provider.py             # pgvector integration
│   │   │   ├── qdrant_provider.py               # Qdrant integration
│   │   │   ├── chroma_provider.py               # ChromaDB integration
│   │   │   ├── s3_provider.py                   # S3 integration
│   │   │   └── minio_provider.py                # MinIO integration
│   │   │
│   │   ├── jobs/
│   │   │   ├── nightly_summarizer.py            # Nightly summarization
│   │   │   ├── archive_old_sessions.py          # Archives old sessions
│   │   │   ├── clean_low_value_memory.py        # Cleans low-value memories
│   │   │   ├── rebuild_embeddings.py            # Rebuilds embeddings
│   │   │   ├── memory_health_check.py           # Memory health monitoring
│   │   │   └── stale_memory_cleanup.py          # Removes stale memory
│   │   │
│   │   └── experiments/
│   │       ├── long_context_tests.py            # Long-context experiments
│   │       ├── memory_ranking_tests.py          # Retrieval-ranking tests
│   │       ├── compression_tests.py             # Compression experiments
│   │       ├── hybrid_memory_tests.py           # Hybrid-memory experiments
│   │       ├── retrieval_benchmarks.py          # Retrieval benchmarks
│   │       └── context_window_tests.py          # Context-window experiments
│   │
│   ├── tools/
│   │   ├── registry.py                          # Central tool registry
│   │   ├── tool_executor.py                     # Executes tools securely
│   │   ├── tool_definitions.py                  # Shared tools registry definition
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
│   │   ├── requirement_planner.py               # Converts requirements into plans
│   │   ├── architecture_planner.py              # Creates architecture plans
│   │   ├── implementation_planner.py            # Creates implementation strategy
│   │   ├── dependency_planner.py                # Resolves dependencies
│   │   ├── parallel_executor.py                 # Executes parallel tasks
│   │   ├── workflow_optimizer.py                # Optimizes workflow execution order
│   │   └── plan_validator.py                    # Validates execution plans
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
│   │   ├── execution_history.py                 # Stores execution history timeline
│   │   ├── state_restorer.py                    # Restores workflow state
│   │   └── checkpoint_cleaner.py                # Cleans stale checkpoints
│   │
│   ├── sandbox/
│   │   ├── docker_runner.py                     # Docker-isolated execution
│   │   ├── vm_runner.py                         # VM-based isolated execution
│   │   ├── restricted_shell.py                  # Restricted shell execution layer
│   │   ├── policy_enforcer.py                   # Enforces sandbox security policies
│   │   ├── filesystem_guard.py                  # Restricts filesystem access
│   │   ├── network_guard.py                     # Restricts external network calls
│   │   ├── execution_monitor.py                 # Monitors runtime safety
│   │   ├── resource_limiter.py                  # CPU/RAM/process usage limiting
│   │   └── sandbox_audit.py                     # Audits sandbox operations
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
│   │   ├── delegation_manager.py                # Handles task delegation
│   │   ├── workflow_coordinator.py              # Coordinates workflow execution
│   │   └── distributed_lock_manager.py          # Prevents execution conflicts
│   │
│   ├── clarification/
│   │   ├── clarification_engine.py              # Decides whether clarification is needed
│   │   ├── requirement_analyzer.py              # Detects missing requirements
│   │   ├── ambiguity_detector.py                # Detects ambiguous prompts/instructions
│   │   ├── risk_question_generator.py           # Generates safety/risk-related questions
│   │   ├── architecture_questioner.py           # Asks architecture/system-design questions
│   │   ├── assumption_validator.py              # Detects unsafe assumptions
│   │   ├── clarification_memory.py              # Stores clarification history
│   │   └── question_priority_ranker.py          # Ranks important clarification questions
│   │
│   ├── learning/
│   │   ├── feedback_store.py                    # Stores user feedback signals
│   │   ├── failure_memory.py                    # Stores failed execution history
│   │   ├── success_patterns.py                  # Stores successful workflows
│   │   ├── workflow_learning.py                 # Learns reusable workflow patterns
│   │   ├── correction_memory.py                 # Stores user corrections
│   │   ├── reinforcement_signals.py             # Tracks positive/negative feedback
│   │   ├── adaptive_prompting.py                # Dynamically improves prompts
│   │   ├── preference_learning.py               # Learns user coding preferences
│   │   ├── execution_learning.py                # Learns from execution outcomes
│   │   ├── ranking_optimizer.py                 # Improves retrieval/ranking over time
│   │   └── learning_metrics.py                  # Tracks learning-system quality
│   │
│   ├── failure_analysis/
│   │   ├── root_cause_analyzer.py               # Performs root-cause analysis
│   │   ├── stacktrace_analyzer.py               # Analyzes runtime stacktraces
│   │   ├── retry_strategy.py                    # Generates retry strategies
│   │   ├── failure_classifier.py                # Categorizes execution failures
│   │   ├── recovery_suggester.py                # Suggests recovery mechanisms
│   │   ├── regression_detector.py               # Detects regressions after fixes
│   │   ├── incident_tracker.py                  # Tracks execution incidents
│   │   └── failure_metrics.py                   # Tracks failure analytics
│   │
│   ├── decision_engine/
│   │   ├── autonomy_controller.py               # Controls autonomous behavior level
│   │   ├── confidence_router.py                 # Routes based on confidence score
│   │   ├── risk_engine.py                       # Calculates execution risk
│   │   ├── approval_decider.py                  # Decides when approval is required
│   │   ├── execution_decider.py                 # Decides whether task can execute
│   │   ├── retrieval_decider.py                 # Decides retrieval strategy
│   │   ├── planning_decider.py                  # Decides planning depth dynamically
│   │   ├── tool_selection_engine.py             # Chooses safest/best tools
│   │   └── fallback_strategy.py                 # Handles safe fallback execution
│   │
│   ├── confidence/
│   │   ├── confidence_scorer.py                 # Calculates confidence score
│   │   ├── uncertainty_detector.py              # Detects uncertain reasoning
│   │   ├── hallucination_probability.py         # Estimates hallucination probability
│   │   ├── retrieval_confidence.py              # Scores retrieval quality confidence
│   │   ├── execution_confidence.py              # Scores execution safety confidence
│   │   ├── answer_verifier.py                   # Verifies generated responses
│   │   ├── confidence_thresholds.py             # Defines confidence thresholds
│   │   └── trust_score.py                       # Calculates system trust score
│   │
│   ├── goals/
│   │   ├── active_goals.py                      # Stores active user goals
│   │   ├── goal_tracker.py                      # Tracks goal progress
│   │   ├── milestone_manager.py                 # Tracks milestone completion
│   │   ├── objective_memory.py                  # Stores goal-related memory
│   │   ├── completion_evaluator.py              # Evaluates goal completion
│   │   ├── dependency_goals.py                  # Tracks dependent goals/tasks
│   │   ├── goal_prioritizer.py                  # Prioritizes objectives dynamically
│   │   └── abandoned_goal_cleaner.py            # Cleans stale/inactive goals
│   │
│   ├── reflection/
│   │   ├── self_critique.py                     # Self-reflection reasoning loop
│   │   ├── reasoning_validator.py               # Validates reasoning quality
│   │   ├── correction_loop.py                   # Attempts self-correction
│   │   ├── confidence_scorer.py                 # Scores reasoning confidence
│   │   ├── hallucination_guard.py               # Detects hallucinated responses
│   │   ├── response_refiner.py                  # Refines weak responses
│   │   ├── critique_memory.py                   # Stores reflection history
│   │   └── retry_reflection.py                  # Re-attempts failed reasoning
│   │
│   ├── approval/
│   │   ├── diff_reviewer.py                     # Reviews generated diffs
│   │   ├── approval_queue.py                    # Human approval workflow queue
│   │   ├── human_gate.py                        # Requires human intervention when risky
│   │   ├── risk_assessor.py                     # Scores execution risk
│   │   ├── safe_execution.py                    # Executes only approved actions
│   │   └── approval_policies.py                 # Defines approval policies
│   │
│   ├── evaluation/
│   │   ├── benchmark_runner.py                  # Runs benchmark evaluations
│   │   ├── prompt_eval.py                       # Evaluates prompt quality
│   │   ├── retrieval_eval.py                    # Evaluates retrieval quality
│   │   ├── hallucination_eval.py                # Measures hallucination rate
│   │   ├── agent_scorecard.py                   # Scores agent performance
│   │   ├── regression_tests.py                  # Prevents behavioral regressions
│   │   ├── memory_eval.py                       # Evaluates memory quality
│   │   ├── execution_eval.py                    # Evaluates execution correctness
│   │   ├── planning_eval.py                     # Evaluates planning quality
│   │   └── autonomous_eval.py                   # Evaluates autonomous behavior
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
│   │   ├── execution_dashboard.py               # Aggregates dashboards
│   │   └── anomaly_detector.py                  # Detects abnormal behavior
│   │
│   ├── runtime/
│   │   ├── workflow_runtime.py                  # Executes long-running workflows
│   │   ├── execution_engine.py                  # Central execution runtime
│   │   ├── task_executor.py                     # Executes atomic tasks
│   │   ├── async_runtime.py                     # Async orchestration runtime
│   │   ├── runtime_scheduler.py                 # Runtime task scheduling
│   │   ├── worker_pool.py                       # Parallel worker management
│   │   ├── execution_supervisor.py              # Supervises workflow execution
│   │   ├── runtime_recovery.py                  # Handles runtime recovery
│   │   ├── runtime_context.py                   # Maintains runtime execution context
│   │   ├── lifecycle_hooks.py                   # Runtime lifecycle hooks
│   │   ├── execution_tracker.py                 # Tracks runtime execution progress
│   │   └── runtime_metrics.py                   # Runtime performance metrics
│   │
│   ├── queue/
│   │   ├── rabbitmq_client.py                   # RabbitMQ integration
│   │   ├── redis_queue.py                       # Redis queue support
│   │   ├── task_dispatcher.py                   # Dispatches tasks to workers
│   │   ├── delayed_queue.py                     # Delayed task execution
│   │   ├── retry_queue.py                       # Retry queue handling
│   │   ├── dead_letter_queue.py                 # Failed-task storage
│   │   ├── priority_queue.py                    # Priority-based task execution
│   │   ├── queue_monitor.py                     # Monitors queue health
│   │   ├── queue_metrics.py                     # Queue-performance metrics
│   │   └── distributed_consumer.py              # Distributed worker consumer
│   │
│   ├── plugins/
│   │   ├── plugin_loader.py                     # Dynamically loads plugins
│   │   ├── plugin_registry.py                   # Registers plugins/tools
│   │   ├── plugin_sandbox.py                    # Isolates plugins securely
│   │   ├── plugin_permissions.py                # Plugin access permissions
│   │   ├── plugin_marketplace.py                # Discovers installable plugins
│   │   ├── plugin_lifecycle.py                  # Plugin install/update/remove
│   │   ├── plugin_validator.py                  # Validates plugin integrity
│   │   ├── plugin_hooks.py                      # Plugin hook/event integration
│   │   ├── plugin_context.py                    # Shared plugin context
│   │   └── plugin_manifest.py                   # Plugin metadata schema
│   │
│   ├── security/
│   │   ├── auth.py                              # Authentication engine
│   │   ├── jwt_manager.py                       # JWT token management
│   │   ├── oauth.py                             # OAuth providers
│   │   ├── rbac.py                              # Role-based access control
│   │   ├── permissions.py                       # Permission system
│   │   ├── api_key_manager.py                   # API-key management
│   │   ├── tenant_security.py                   # Multi-tenant isolation
│   │   ├── secrets_manager.py                   # Secure secret handling
│   │   ├── session_security.py                  # Secure session management
│   │   ├── encryption.py                        # Encryption utilities
│   │   ├── csrf_protection.py                   # CSRF security protection
│   │   └── security_audit.py                    # Security audit logging
│   │
│   ├── tenancy/
│   │   ├── tenant_manager.py                    # Handles tenant lifecycle
│   │   ├── tenant_context.py                    # Injects tenant context
│   │   ├── tenant_isolation.py                  # Prevents cross-tenant leakage
│   │   ├── billing_context.py                   # Tracks tenant usage/billing
│   │   ├── tenant_memory_router.py              # Tenant-aware memory routing
│   │   ├── tenant_registry.py                   # Tenant metadata registry
│   │   ├── tenant_config.py                     # Tenant-specific configuration
│   │   ├── tenant_limits.py                     # Tenant quota restrictions
│   │   └── tenant_audit.py                      # Tenant activity auditing
│   │
│   ├── billing/
│   │   ├── usage_tracker.py                     # Tracks usage metrics
│   │   ├── token_billing.py                     # Tracks token costs
│   │   ├── provider_costs.py                    # Tracks provider billing
│   │   ├── quota_enforcer.py                    # Enforces usage quotas
│   │   ├── subscription_manager.py              # Handles plans/subscriptions
│   │   ├── invoice_generator.py                 # Generates invoices/reports
│   │   ├── billing_metrics.py                   # Billing analytics
│   │   ├── pricing_engine.py                    # Dynamic pricing logic
│   │   └── usage_forecasting.py                 # Predicts future usage
│   │
│   ├── deployment/
│   │   ├── deployment_orchestrator.py           # Deploys applications/services
│   │   ├── kubernetes_deployer.py               # Kubernetes deployment engine
│   │   ├── docker_builder.py                    # Builds container images
│   │   ├── release_manager.py                   # Release orchestration
│   │   ├── canary_manager.py                    # Canary deployment handling
│   │   ├── rollback_deployer.py                 # Rollback automation
│   │   ├── environment_manager.py               # Environment configuration
│   │   ├── deployment_validator.py              # Validates deployments
│   │   ├── deployment_monitor.py                # Tracks deployment health
│   │   └── deployment_audit.py                  # Deployment audit logs
│   │
│   ├── cicd/
│   │   ├── github_actions.py                    # GitHub Actions integration
│   │   ├── pipeline_generator.py                # Generates CI/CD pipelines
│   │   ├── deployment_validator.py              # Validates deployments
│   │   ├── security_scanner.py                  # CI security scanning
│   │   ├── dependency_updater.py                # Dependency update automation
│   │   ├── release_notes_generator.py           # Generates release notes
│   │   ├── build_optimizer.py                   # Optimizes build execution
│   │   ├── flaky_test_detector.py               # Detects unstable tests
│   │   ├── ci_failure_analyzer.py               # Analyzes CI failures
│   │   └── pipeline_metrics.py                  # CI/CD analytics
│   │
│   ├── knowledge_extraction/
│   │   ├── code_knowledge_extractor.py          # Extracts knowledge from code
│   │   ├── documentation_extractor.py           # Extracts documentation automatically
│   │   ├── architecture_extractor.py            # Extracts architecture patterns
│   │   ├── workflow_extractor.py                # Learns workflows automatically
│   │   ├── incident_extractor.py                # Learns from incidents/failures
│   │   ├── semantic_tagger.py                   # Adds semantic metadata
│   │   ├── repository_summarizer.py             # Summarizes repositories/projects
│   │   ├── changelog_extractor.py               # Generates semantic changelogs
│   │   └── knowledge_graph_builder.py           # Builds knowledge graph automatically
│   │
│   ├── simulation/
│   │   ├── dry_run_engine.py                    # Simulates execution safely
│   │   ├── impact_analyzer.py                   # Predicts execution impact
│   │   ├── dependency_simulator.py              # Simulates dependency effects
│   │   ├── token_simulator.py                   # Predicts token consumption
│   │   ├── runtime_simulator.py                 # Simulates runtime execution
│   │   ├── risk_simulator.py                    # Simulates risk scenarios
│   │   ├── deployment_simulator.py              # Simulates deployments
│   │   ├── sandbox_simulator.py                 # Simulates sandbox execution
│   │   └── simulation_metrics.py                # Simulation-performance metrics
│   │
│   ├── compliance/
│   │   ├── policy_engine.py                     # Enterprise policy enforcement
│   │   ├── pii_detector.py                      # Detects sensitive information
│   │   ├── compliance_checker.py                # Checks compliance rules
│   │   ├── data_governance.py                   # Handles data governance
│   │   ├── audit_compliance.py                  # Audit/compliance tracking
│   │   ├── retention_compliance.py              # Compliance-aware retention
│   │   ├── gdpr_handler.py                      # GDPR compliance utilities
│   │   ├── security_compliance.py               # Security-compliance checks
│   │   ├── compliance_reports.py                # Generates compliance reports
│   │   └── legal_hold_manager.py                # Handles legal retention policies
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
│   ├── model_intelligence/
│   │   ├── model_profiler.py                    # Benchmarks model performance
│   │   ├── capability_router.py                 # Routes by model strengths
│   │   ├── latency_optimizer.py                 # Optimizes latency
│   │   ├── quality_router.py                    # Routes by output quality
│   │   ├── local_model_selector.py              # Chooses local GGUF models
│   │   ├── quantization_manager.py              # Handles quantized models
│   │   ├── context_optimizer.py                 # Optimizes model context
│   │   ├── fallback_chains.py                   # Multi-model fallback chains
│   │   ├── provider_selector.py                 # Selects optimal provider
│   │   ├── token_optimizer.py                   # Optimizes token usage
│   │   ├── model_health_monitor.py              # Tracks model health/status
│   │   └── inference_metrics.py                 # Tracks inference analytics
│   │
│   ├── multimodal/
│   │   ├── whisper_engine.py                    # Speech-to-text integration
│   │   ├── tts_engine.py                        # Text-to-speech integration
│   │   ├── image_reasoning.py                   # Vision reasoning engine
│   │   ├── screenshot_parser.py                 # Screenshot/code parsing
│   │   ├── video_analysis.py                    # Video understanding
│   │   ├── realtime_voice_session.py            # Realtime voice conversations
│   │   ├── image_embedding_service.py           # Image embeddings
│   │   ├── ocr_engine.py                        # OCR text extraction
│   │   ├── multimodal_router.py                 # Routes multimodal requests
│   │   └── media_preprocessor.py                # Media preprocessing pipeline
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
│   └── os/
│       ├── kernel.py                            # Core orchestration kernel
│       ├── scheduler.py                         # Global scheduling engine
│       ├── memory_bus.py                        # Shared memory communication bus
│       ├── capability_registry.py               # Tracks system capabilities
│       ├── lifecycle_manager.py                 # Manages system lifecycle
│       ├── orchestration_kernel.py              # Coordinates all subsystems
│       ├── system_health_manager.py             # Global health monitoring
│       ├── task_supervisor.py                   # Supervises global tasks
│       ├── service_discovery.py                 # Discovers active services
│       ├── global_context.py                    # Shared global system context
│       ├── orchestration_router.py              # Routes subsystem orchestration
│       └── operating_state.py                   # Maintains global operating state
│
├── storage/                                     # Persistent storage layer
├── infrastructure/                              # Infrastructure and deployment configuration
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
