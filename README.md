# Exercise Movement Analysis (EMA) System

The Exercise Movement Analysis (EMA) System is a framework for analyzing
exercise movements, providing automated feedback, and evaluating exercise form.
This system combines advanced motion capture processing, movement analysis,
and natural language feedback generation.

## System Overview

The EMA System consists of several core modules:

- **Core Processing**: Fundamental utilities for motion capture data processing
- **Feature Extraction**: Movement analysis and exercise signature computation
- **Exercise Segmentation**: Automated detection and segmentation of exercise repetitions
- **Statistical Coach**: Movement comparison and deviation detection
- **Feedback Generation**: Natural language feedback for exercise form improvement
- **Evaluation Framework**: Comprehensive tools for system performance assessment

## Key Features

### Motion Analysis

- Load and process motion capture data from multiple sources
- Calculate joint angles using quaternion and vector-based approaches
- Detect and segment exercise repetitions automatically
- Generate exercise signatures for movement comparison

### Exercise Assessment

- Compare trainee movements against reference performances
- Identify active and passive movement features
- Detect form deviations and alignment issues
- Generate statistical analysis of performance

### Feedback Generation

- Provide natural language feedback on exercise form
- Generate per-repetition detailed feedback
- Identify consistent issues across repetitions
- Offer specific improvement suggestions

### Evaluation Tools

- Comprehensive evaluation framework for all system components
- Support for multiple datasets and sensor types
- Statistical analysis of system performance
- Visualization tools for result analysis

## Installation

### Local Installation

```bash
# Clone the repository
git clone https://github.com/physiomio/src.git

# Install dependencies
pip install -r requirements.txt
```

### Docker Container

The system includes a Dockerfile for containerized deployment:

```bash
# Build Docker image
docker build -t ema-system .

# Run container
docker run -it ema-system
```

### AWS SageMaker Deployment

The repository includes scripts for deploying and
running training jobs on AWS SageMaker:

- `Dockerfile` and `entrypoint.py`: Container definition for SageMaker
- `create_training_job.py`: Script to configure and launch SageMaker training jobs
- `build_and_push.sh`: Utility script to build and push Docker image to ECR

To deploy on SageMaker:

```bash
# Build and push Docker image to ECR
./build_and_push.sh

# Create and start training job
python create_training_job.py
```

## Quick Start

```python
from ema.pipeline import ExerciseAnalysisPipeline
from ema.core import MotionDataLoader
from ema.feedback import FeedbackGenerator

# Initialize pipeline
pipeline = ExerciseAnalysisPipeline(
    base_percentage=0.2,
    segmentation_strategy="hybrid",
    visualize=True
)

# Process trainer reference
trainer_results = pipeline.process_trainer_data("trainer.parquet")

# Analyze trainee performance
trainee_results = pipeline.process_trainee_data(
    "trainee.parquet",
    report_file="analysis_report.txt"
)

# Generate feedback
feedback = pipeline.generate_feedback(trainee_results)
```

## Module Structure

### 1. Core Processing

- Motion data loading and validation
- Joint angle calculations
- Basic movement detection
- Logging infrastructure

### 2. Feature Extraction

- Angular feature calculation
- Energy-based feature classification
- Exercise signature computation
- Movement pattern analysis

### 3. Exercise Segmentation

- Initial period detection
- Repetition finding
- Boundary optimization
- Multiple segmentation strategies

### 4. Statistical Coach

- Reference movement comparison
- Deviation detection
- Performance analysis

### 5. Feedback Generation

- Natural language processing
- Context-aware feedback
- Improvement suggestions

### 6. Evaluation Framework

- Segmentation evaluation
- Signature analysis
- Coach performance assessment
- System-wide metrics

## Data Requirements

The system expects motion capture data in parquet format with:

- Timestamp column
- Joint position data (x,y,z coordinates)
- Joint rotation data (quaternions)
- Consistent naming conventions for joints

## Best Practices

1. **Data Quality**
   - Ensure clean, calibrated motion capture data
   - Validate trainer reference data quality
   - Check for missing markers or tracking issues

2. **System Configuration**
   - Start with default parameters
   - Adjust base_percentage based on exercise complexity
   - Use hybrid segmentation for complex movements
   - Enable visualization during development

3. **Analysis**
   - Review visualization plots
   - Validate feedback against video recordings
   - Monitor system performance metrics

## Testing

The system includes a comprehensive test suite located in
`ema_system/tests/`. To run the tests:

```bash
# Run all tests
pytest ema_system/tests/

# Run tests with coverage report
pytest --cov=ema_system tests/
```
