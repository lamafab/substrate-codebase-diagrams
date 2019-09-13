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
    $wasm_exec -> $wasmi_mod: from_buffer()
        activate $wasmi_mod
        $wasmi_mod <-- $wasm_exec: TODO
        deactivate $wasmi_mod


    ' START "instantiate_module" section
    $wasm_exec -> $wasm_exec: instantiate_module()
        activate $wasm_exec #005500
        create $wasmi_mod_inst
        $wasm_exec -> $wasmi_mod_inst: new()
            activate $wasmi_mod_inst
            $wasmi_mod_inst --> $wasm_exec
            deactivate $wasmi_mod_inst

        $wasm_exec -> $wasm_exec: get_heap_base()
            activate $wasm_exec
            $wasm_exec -> $wasmi_mod_inst: not_started_instance()
                activate $wasmi_mod_inst
                $wasm_exec <-- $wasmi_mod_inst: TODO
                deactivate $wasmi_mod_inst
            deactivate $wasm_exec

        $wasm_exec -> $wasm_exec: gem_mem_instance()
            activate $wasm_exec
            $wasm_exec -> $wasmi_mod_inst: not_started_instance()
                activate $wasmi_mod_inst
                $wasm_exec <-- $wasmi_mod_inst: TODO
                deactivate $wasmi_mod_inst
            deactivate $wasm_exec

        create $wasmi_mod_ref
        $wasm_exec -> $wasmi_mod_ref: assert_no_start()
            activate $wasmi_mod_ref
            $wasm_exec <-- $wasmi_mod_ref
            deactivate $wasmi_mod_ref

        $wasm_exec <-- $wasm_exec: TODO
        deactivate $wasm_exec
    ' END "instantiate_module" section

    $wasm_exec -> $wasm_exec: call_in_wasm_module()
        activate $wasm_exec #005500
        $wasm_exec -> $wasm_exec: call_in_wasm_module_with_custom_signature()
            activate $wasm_exec
            $wasm_exec -> $wasm_exec: get_mem_instance()
                activate $wasm_exec
                $wasm_exec <-- $wasm_exec: TODO
                deactivate $wasm_exec

            $wasm_exec -> $wasmi_mod_ref: export_by_name()
                activate $wasmi_mod_ref
                $wasm_exec <-- $wasmi_mod_ref
                deactivate $wasmi_mod_ref

            ' let heap_base = Self::get_heap_base(module_instance)?;
            $wasm_exec -> $wasm_exec: get_heapbase()
                activate $wasm_exec
                $wasm_exec <-- $wasm_exec: TODO
                deactivate $wasm_exec

            ' let mut fec = $func_exec::new()
            create $func_exec
            $wasm_exec -> $func_exec: new()
                activate $func_exec

                create $sandb_store
                $func_exec -> $sandb_store: new()
                    activate $sandb_store
                    $func_exec <-- $sandb_store
                    deactivate $sandb_store

                create $alloc_fbha
                $func_exec -> $alloc_fbha: new()
                    activate $alloc_fbha
                    $func_exec <-- $alloc_fbha
                    deactivate $alloc_fbha

                $wasm_exec <-- $func_exec: TODO
                deactivate $func_exec

            ' let parameters = create_parameters()
            $wasm_exec -> $wasm_exec: create_parameters()
                activate $wasm_exec
                $wasm_exec <-- $wasm_exec: TODO
                deactivate $wasm_exec

            ' let result = runtime_io::with_externalities


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