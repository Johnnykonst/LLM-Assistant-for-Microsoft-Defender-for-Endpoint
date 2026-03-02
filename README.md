# LLM-Assistant-for-Microsoft-Defender-for-Endpoint
Design and implementation of an LLM-based Python script for identifying public IOCs from APT attacks and generating detection rules in MDE.

Python-Based LLM Assistant for MITRE-Aware KQL Generation

This script implements a Python-based assistant that integrates structured
threat intelligence from OpenCTI with a Large Language Model (LLM) in order
to automatically generate Kusto Query Language (KQL) detection rules for
Microsoft Defender for Endpoint (MDE).

The assistant retrieves MITRE ATT&CK technique metadata via the OpenCTI
GraphQL API, constructs constrained prompts for the LLM, post-processes
the generated KQL to ensure schema compatibility, and supports iterative
human-in-the-loop refinement.