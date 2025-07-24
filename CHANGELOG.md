# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [1.2.0] - 2025-01-24

### 🚀 Major Performance Enhancements

#### Added
- **Smart Data Volume Management**
  - Automatic row count estimation before data fetching
  - Interactive warning system for queries returning >2,500 rows
  - Specific optimization suggestions to reduce data volume
  - `estimate_only` parameter to get row counts without fetching data

- **Server-Side Processing Optimizations**
  - Intelligent server-side aggregation using GA4's `MetricAggregation.TOTAL`
  - Smart sorting with `OrderBy` parameters (recent dates first, highest values first)
  - Automatic aggregation detection for queries without date dimensions

- **Enhanced User Control Parameters**
  - `proceed_with_large_dataset` - Override warnings for large datasets
  - `limit` - Set maximum number of rows to return
  - `enable_aggregation` - Control server-side aggregation behavior
  - `estimate_only` - Get row estimates without data fetching

- **Response Metadata & Transparency**
  - Applied optimizations tracking in response metadata
  - Total vs returned row counts when limits are applied
  - Clear indicators when aggregation or sorting is applied

#### Changed
- Updated FastMCP dependency to `>=2.0.0` for better performance
- Enhanced `get_ga4_data` function with backward-compatible optimization parameters
- Improved error handling with graceful degradation when optimizations fail

#### Fixed
- **Context Window Crash Prevention** - Eliminates crashes from large datasets
- **Memory Usage Optimization** - Reduces memory footprint for large queries
- **API Rate Limit Management** - Better handling of GA4 API quotas

### 🔧 Technical Improvements
- Added helper functions `_get_smart_sorting()` and `_should_aggregate()`
- Enhanced response formatting with metadata for transparency
- Improved error messages and debugging information

### 📚 Documentation
- Added comprehensive optimization features section to README
- Updated usage examples with optimization scenarios
- Added troubleshooting guide for large dataset handling

## [1.0.11] - Previous Release
- Base functionality with 200+ GA4 dimensions and metrics
- Core MCP server implementation
- Basic data retrieval capabilities

---

### Migration Guide

**From v1.0.x to v1.2.0:**

No breaking changes! All existing queries will continue to work exactly as before. New optimization features are automatically enabled with sensible defaults.

**New Features You Can Use:**
```python
# Get row count estimate before fetching
get_ga4_data(dimensions=["city", "date"], estimate_only=True)

# Override warnings for large datasets
get_ga4_data(dimensions=["city", "date"], proceed_with_large_dataset=True)

# Set custom row limits
get_ga4_data(dimensions=["city"], limit=100)

# Disable automatic aggregation
get_ga4_data(dimensions=["month"], enable_aggregation=False)
```