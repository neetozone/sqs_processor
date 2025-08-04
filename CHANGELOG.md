# Changelog

All notable changes to the SQS Processor gem will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [0.1.3] - 2024-01-01

### Added
- **Immediate Graceful Shutdown**: Like Puma, the processor now responds immediately to SIGTERM, SIGINT, and SIGQUIT signals
- **Signal Interruption**: Immediately interrupts any blocking operations (SQS polling, sleep) when shutdown signals are received
- **Interrupt Exception Handling**: Catches and handles Interrupt exceptions at multiple levels for clean shutdown

### Changed
- **Shutdown Response Time**: Reduced from 20+ seconds to immediate response
- **Signal Handler Enhancement**: Added Thread.main.raise Interrupt.new to force immediate interruption
- **Error Handling**: Added specific handling for Interrupt exceptions in main loop and message reception

## [0.1.2] - 2024-01-01

### Added
- **Graceful Shutdown**: Handles SIGTERM, SIGINT, and SIGQUIT signals gracefully
- **Signal Handlers**: Setup handlers for termination signals
- **Shutdown State Management**: Added @shutdown_requested flag and related methods
- **Shutdown Check Points**: Added shutdown checks in main loop and message processing

### Changed
- **Reduced Polling Timeouts**: SQS polling reduced from 20s to 3s, loop delay reduced to 0.5s
- **Faster Shutdown Response**: Processor now responds within 3-4 seconds to shutdown signals

## [0.1.1] - 2024-01-01

### Added
- **AWS Credentials Support**: Direct AWS credentials can be passed to constructor
- **Flexible Constructor**: Supports both AWS credentials and pre-configured SQS client
- **Session Token Support**: Added support for AWS session tokens for temporary credentials

### Changed
- **Constructor Parameters**: Added aws_access_key_id, aws_secret_access_key, aws_session_token, aws_region parameters
- **SQS Client Setup**: Enhanced setup_sqs_client method to handle multiple credential sources
- **Documentation**: Updated README with both usage patterns

## [0.1.0] - 2024-01-01

### Added
- **Initial Release**: SQS Processor gem with core functionality
- **Gem Structure**: Proper Ruby gem structure with lib/, spec/, examples/ directories
- **SQS Integration**: AWS SQS client integration with long polling
- **Message Processing**: Hook-based message processing with handle_message method
- **Error Handling**: Robust error handling with message retention on failure
- **Logging**: Comprehensive logging with configurable levels
- **Batch Processing**: Configurable batch processing with max_messages parameter
- **Visibility Timeout**: Configurable message visibility timeout
- **Environment Variables**: Support for DATA_SYNC_ prefixed environment variables
- **Documentation**: Comprehensive README with usage examples
- **Testing**: Basic RSpec setup and tests
- **Code Style**: RuboCop configuration for consistent code style
- **License**: MIT License

### Features
- Long polling for efficient SQS message retrieval
- Batch processing with configurable batch sizes
- Hook-based message processing for custom logic
- Graceful error handling with message retention
- Comprehensive logging with timestamps
- Environment variable configuration
- Custom processor subclassing support
