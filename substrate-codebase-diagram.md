### uml: class diagram
```plantuml
@startuml
!$wasm_exec = "WasmExecutor"
!$wasmi_mod = '"wasmi::Module"'
!$wasmi_mod_inst = '"wasmi::ModuleInstance"'
!$wasmi_mod_ref = '"wasmi::ModuleRef"'
!$func_exec = "FunctionExecutor"
!$alloc_fbha = '"allocator::FreeingBumpHeapAllocator"'
!$sandb_store = '"sandbox::Store"'

'autoactivate on
activate $wasm_exec
$wasm_exec -> $wasm_exec: call()
    activate $wasm_exec

    ' Call to Module
    'hnote over $wasm_exec: A Note
    $wasm_exec -> $wasmi_mod ++: from_buffer()
        return

    ' START "instantiate_module" section
    $wasm_exec -> $wasm_exec ++ #005500: instantiate_module()
        create $wasmi_mod_inst
        $wasm_exec -> $wasmi_mod_inst ++: new()
            return

        $wasm_exec -> $wasm_exec ++: get_heap_base()
            $wasm_exec -> $wasmi_mod_inst ++: not_started_instance()
                return
            return

        $wasm_exec -> $wasm_exec ++: gem_mem_instance()
            $wasm_exec -> $wasmi_mod_inst ++: not_started_instance()
                return
            return

        create $wasmi_mod_ref
        $wasm_exec -> $wasmi_mod_ref ++: assert_no_start()
            return

        return
    ' END "instantiate_module" section

    $wasm_exec -> $wasm_exec ++ #005500: call_in_wasm_module()
        $wasm_exec -> $wasm_exec ++: call_in_wasm_module_with_custom_signature()
            $wasm_exec -> $wasm_exec ++: get_mem_instance()
                return

            $wasm_exec -> $wasmi_mod_ref ++: export_by_name()
                return

            ' let heap_base = Self::get_heap_base(module_instance)?;
            $wasm_exec -> $wasm_exec ++: get_heapbase()
                return

            ' let mut fec = $func_exec::new()
            create $func_exec
            $wasm_exec -> $func_exec ++: new()
                create $sandb_store
                $func_exec -> $sandb_store ++: new()
                    return

                create $alloc_fbha
                $func_exec -> $alloc_fbha ++: new()
                    return

                return

            ' let parameters = create_parameters()
            $wasm_exec -> $wasm_exec ++: create_parameters()
                return

            ' let result = runtime_io::with_externalities

            return

'... todo

@enduml
```

    class $wasm_exec {
        // Executes the provided code in a sandboxed wasm runtime
        ==
        + new()
        + call()
        + call_with_custom_signature()
        + get_mem_instance()
        + get_heap_base()
        + call_in_wasm_module()
        + call_in_wasm_module_with_custom_signature()
        + instantiate_module()
    }