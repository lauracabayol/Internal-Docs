# Python Unit Testing Guide with pytest

## Overview
This guide outlines our Python unit testing practices using pytest, a feature-rich testing framework that makes writing and running tests simple and efficient.

## Testing Framework
We use `pytest` as our primary testing framework. To install:

## Project Structure
project/
├── src/
│ ├── init.py
│ └── module.py
└── tests/
├── init.py
├── conftest.py # shared pytest fixtures
└── test_module.py

## Naming Conventions
- Test files should be prefixed with `test_` (e.g., `test_user_service.py`)
- Test functions should be prefixed with `test_`
- Test classes should be prefixed with `Test` (e.g., `TestUserService`)
- Fixture functions should have descriptive names indicating their purpose

## Writing Tests

### Basic Test Structure
```python
def test_function_name():
# Arrange
expected = "expected_value"
# Act
result = function_to_test()
# Assert
assert result == expected
```

## Example

### Fixtures
A fixture is a function that provides test data or test objects that can be reused across multiple tests. Fixtures are defined using the `@pytest.fixture` decorator.

```python
def sample_catalogue():
    """Create a small sample catalogue for testing."""
    np.random.seed(42)
    n_samples = 10
    
    # Create dummy data that matches the structure needed
    data = {
        'observed_redshift_gal': np.random.uniform(0, 1, n_samples),
    }
    
    # Add PAU narrow bands
    for x in np.arange(455, 855, 10):
        data[f'pau_nb{x}'] = np.random.uniform(1000, 5000, n_samples)
    
    return pd.DataFrame(data)
```
### Tests
```python
def test_create_simulated_images_basic(sample_catalogue, temp_output_dir):
    """Test basic functionality of create_simulated_images."""
    bands = [f'pau_nb{x}' for x in np.arange(455, 855, 10)]
    
    simulator = create_simulated_images(
        catalogue=sample_catalogue,
        Ngals=2,
        bands=bands,
        add_poisson=True,
        add_psf=True,
        add_constant_background=True,
        use_dask=False,
        num_exposures=1,
        output_dir=temp_output_dir
    )
    
    assert simulator is not None
    assert hasattr(simulator, '_get_photometry')
    assert hasattr(simulator, '_get_morphology')
    assert hasattr(simulator, '_create_simulated_galaxy')
```

## Running Tests
### Install
```bash
pip install pytest
```

### Run
To run the tests, use the following command:
```bash
pytest /path/to/test/file.py -v
```
