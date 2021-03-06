tink_module(prf)

tink_cc_library(
  NAME hkdf_prf_key_manager
  SRCS hkdf_prf_key_manager.h
  DEPS
    tink::core::key_type_manager
    tink::core::input_stream
    tink::core::key_type_manager
    tink::subtle::subtle
    tink::subtle::prf::hkdf_streaming_prf
    tink::subtle::prf::streaming_prf
    tink::util::constants
    tink::util::enums
    tink::util::secret_data
    tink::util::status
    tink::util::statusor
    tink::util::validation
    tink::proto::common_cc_proto
    tink::proto::hkdf_prf_cc_proto
    tink::proto::tink_cc_proto
    absl::memory
    absl::strings
)

tink_cc_library(
  NAME prf_config
  SRCS
    prf_config.cc
    prf_config.h
  DEPS
    tink::prf::hkdf_prf_key_manager
    tink::core::registry
    tink::util::status
    tink::proto::tink_cc_proto
)

tink_cc_library(
  NAME prf_key_templates
  SRCS
    prf_key_templates.h
    prf_key_templates.cc
  DEPS
    tink::proto::aes_cmac_prf_cc_proto
    tink::proto::hkdf_prf_cc_proto
    tink::proto::hmac_prf_cc_proto
    tink::proto::tink_cc_proto
    absl::memory
)

tink_cc_library(
  NAME prf_set
  SRCS
    prf_set.h
    prf_set.cc
  DEPS
    tink::util::statusor
    absl::strings
)

tink_cc_test(
  NAME hkdf_prf_key_manager_test
  SRCS hkdf_prf_key_manager_test.cc
  DEPS
    tink::prf::hkdf_prf_key_manager
    tink::subtle::prf::hkdf_streaming_prf
    tink::subtle::prf::streaming_prf
    tink::subtle::subtle
    tink::util::input_stream_util
    tink::util::secret_data
    tink::util::test_matchers
    tink::util::test_util
    tink::proto::common_cc_proto
    gmock
)

tink_cc_test(
  NAME prf_key_templates_test
  SRCS prf_key_templates_test.cc
  DEPS
    tink::prf::hkdf_prf_key_manager
    tink::prf::prf_key_templates
    tink::util::test_matchers
    gmock
)

tink_cc_test(
  NAME prf_set_test
  SRCS prf_set_test.cc
  DEPS
    tink::prf::prf_set
    tink::util::statusor
    absl::memory
    absl::strings
    gmock
)
